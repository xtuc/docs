---
title: Getting started with Byte Arena
include_js:
    - https://cdnjs.cloudflare.com/ajax/libs/prism/1.8.4/components/prism-docker.min.js
---

We will be going through the implementation of a basic agent for Byte Arena.

While your agent can be coded in whatever programming language you like, this section will show you to implement one in JavaScript.

# Prerequisites

* You have installed the [Byte Arena CLI](/doc/the-bytearena-cli) `ba`.
* You have a running Docker daemon (please refer to [Docker's documentation](https://docs.docker.com/) to install it if not).
* You know your way with JavaScript.

# Overview

We are about to:

* Scaffold the source code of your agent to get you started quickly
* Build the agent to make it usable in a Byte Arena game
* Launch a game with your new agent and watch the live visualisation in your browser
* Explore the source code of the agent and explain the different parts
* Modify the source code of the agent to implement a basic obstacle avoidance

# Scaffolding the source code of an agent

`ba` is the name of the Byte Arena command line interface (CLI).

Use it to scaffold the code for your first agent.

```sh
$ ba generate nodejs
```

This command will generate a directory containing the nodejs source code of a basic agent.

Example:

<script type="text/javascript" data-rows="40" src="https://asciinema.org/a/N2YzvXPTWoZI4rBvdpu8LkfI2.js" id="asciicast-N2YzvXPTWoZI4rBvdpu8LkfI2" async></script>

In this example, a directory named `powerful-jennet` has been generated, and the code it contains built in a docker container under the same name.

# Building the agent

You need to build the source code of your agent to make it usable in Byte Arena.
Building an agent means producing a runnable docker container with the agent code.

As we've seen in the previous example, the scaffolding operation has already built the agent for us.

If you want to rebuild it though, you need to issue this command in the folder containing your agent source code:

```sh
$ ba build
```

Alternatively, you can also use docker to build your agent:

```sh
$ docker build -t my-agent-name .
```

This will ask docker to build a container with your code (the `.` folder) and tag it with the desired name.

Note: `ba build` is the recommended way of building, as it does some more checks before building the agent (like checking for the presence of docker instructions that are forbidden on the Byte Arena online platform; see `agent-container.md`)

# Giving it a ride

The agent you just built is already able to fly!

Try it with this command (replace `powerful-jennet` with the name of your agent):

```sh
$ ba train -agent powerful-jennet
```

<script type="text/javascript" data-rows="40" src="https://asciinema.org/a/JwmtBpH9wP9xNqSegw9UC6dhm.js" id="asciicast-JwmtBpH9wP9xNqSegw9UC6dhm" async></script>

A browser should open at http://localhost:8080/arena/1, displaying the Byte Arena visualization, where you'll find your agent.

<video controls="controls" muted style="width: 100%; height: auto; margin: 1em 0;">
    <source type="video/mp4" src="https://s3.eu-central-1.amazonaws.com/bytearena-public/hexagon60.mp4"></source>
    <p>Your browser does not support the video element.</p>
</video>

Once the game is running, the game log displays a stream of messages informing about the state of the game (lines prefixed by `[game]`), and showing the output of your agents on their stdout (lines prefixed by `[agent]`).

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
# Receiving the environment

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


# Draft

- [Create your container](agent-container)
- [The Bytearena CLI](the-bytearena-cli)


- [Create your first agent](your-first-agent)
    - [Connect to the game server](your-first-agent#comm)
    - [Build your agent](your-first-agent#build)
    - [Taking actions](your-first-agent#take-actions)
    - [Receiving the environment](your-first-agent#perception)