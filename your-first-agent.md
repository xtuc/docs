---
title:  Create your first agent
author: Sven Sauleau, Jérôme Schneider
date:   2017-11-16
include_js:
    - https://cdnjs.cloudflare.com/ajax/libs/prism/1.8.4/components/prism-docker.min.js
---

We will be going through the implementation of a basic agent for Byte Arena.

While your agent can be coded in whatever programming language you like, this section will teach you to implement one in JavaScript.

# Prerequisite

- You have installed the [Byte Arena CLI](/doc/the-bytearena-cli).

- You have a running Docker daemon (please refer to [Docker's documentation](https://docs.docker.com/) to install it if not).

- You know JavaScript.

# Scaffolding your agent

`ba` is the name of the Byte Arena command line interface (CLI).

Use it to generate your first agent code.

```sh
$ ba generate nodejs
```

This command will generate a directory containing the nodejs source code of a basic agent.

Example:

```sh
$ ba generate nodejs
sweet-tarpon has been created
===
=== 🤖  Welcome! I'm the Byte Arena Builder Bot (the local one)
===

=== Building your agent now.

Step 1/8 : FROM node:7
 ---> d9aed20b68a4
Step 2/8 : ENV NPM_CONFIG_LOGLEVEL warn
 ---> Using cache
 ---> bc3d1790a08b
Step 3/8 : WORKDIR /usr/app
 ---> Using cache
 ---> 0047f1426d8f
Step 4/8 : COPY package.json /usr/app/
 ---> Using cache
 ---> 7fbfeb994c31
Step 5/8 : RUN npm install
 ---> Using cache
 ---> 88d69714e082
Step 6/8 : COPY . /usr/app
 ---> Using cache
 ---> 257fe08eed43
Step 7/8 : RUN npm run build
 ---> Using cache
 ---> b946fb1bb52e
Step 8/8 : CMD [ "npm", "start" ]
 ---> Using cache
 ---> 37ca9dc1e5d7
Successfully built 37ca9dc1e5d7
Successfully tagged sweet-tarpon:latest

===
=== ✅  Your agent has been built. Let'em know who's the best!
===    Its name is: sweet-tarpon
===
```

In this example, a directory named `sweet-tarpon` has been produced, and it's code built in a docker container with the same name.

# Giving it a ride

The agent you just built is already able to run!

Try it with this command (replace `sweet-tarpon` with the name of your agent):

```
$ ba train -agent sweet-tarpon
[log] Register agent sweet-tarpon
[log] Listen
[log] Server listening on port 51081
[log] Starting agent containers
[log] Spawning agent 1f9308d9-f475-40e3-8113-97e74910975a

Game running at http://localhost:8080/arena/1

[agent] [sweet-tarpon:latest]
[agent] [sweet-tarpon:latest] > @ start /usr/app
[agent] [sweet-tarpon:latest] > node dist
[agent] [sweet-tarpon:latest]
[log] Agents are ready; starting in 1 second
[game] Tick 0; 15.635 ms mean; 15.635 ms last; 26 goroutines
[game] Tick 20; 0.300 ms mean; 0.328 ms last; 26 goroutines
[game] Tick 40; 0.328 ms mean; 0.186 ms last; 26 goroutines
[game] Tick 60; 0.325 ms mean; 0.434 ms last; 26 goroutines
[game] Tick 80; 0.930 ms mean; 0.313 ms last; 26 goroutines
[game] Tick 100; 0.296 ms mean; 0.283 ms last; 26 goroutines
[game] Tick 120; 0.293 ms mean; 0.378 ms last; 26 goroutines
[game] Tick 140; 0.304 ms mean; 0.277 ms last; 26 goroutines
[...]
```

A browser should open at http://localhost:8080/arena/1, displaying the Byte Arena visualization, where you'll find your agent.

> TODO:image here

You can stop the game by pressing `Ctrl+c` on the command line.

> TODO: Refac the doc here, yo make a smooth transition between the scaffolding and the code exploration / modification.

<a name="comm"></a>
# Connection to the game server

Here is a boilerplate to etablish the connection to the game server:

```js
import {comm} from 'bytearena-sdk';

const agent = comm.connect();
```

At this point you can already launch the trainer with your agent.

<a name="build"></a>
# Building your agent

In the root directory of your program, run the following command:

```sh
$ ba build [AGENT_DIRNAME]
```

<a name="take-actions"></a>
# Taking actions

Your agent can take actions by calling the `takeActions` method:


```js
import {vector} from 'bytearena-sdk';

const Vector2 = vector.Vector2;

const force = new Vector2(0, 1);
actions.push({ method: 'steer', arguments: force.toArray(5) });

agent.takeActions(actions);
```

The supported methods are: `steer` and `shoot`.

<a name="perception"></a>
# Subscribe to the perception

You can listen to the perception events sent by the game server every tick:

```js
agent.on('perception', perception => {
  // Do something
});
```

You can find the full documentation about the perception [here](/doc/understanding-the-perception).

# The complete example

```js
import {vector, comm} from 'bytearena-sdk';

const Vector2 = vector.Vector2;
const agent = comm.connect();

agent.on('perception', perception => {
  const actions = [];

  const force = new Vector2(0, 1);

  actions.push({ method: 'steer', arguments: force.toArray(5) });

  // Pushing batch of mutations
  agent.takeActions(actions);
});
```
