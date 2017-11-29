---
title: Create your first agent
include_js:
    - https://cdnjs.cloudflare.com/ajax/libs/prism/1.8.4/components/prism-docker.min.js
---

We will be going through the implementation of a basic agent for Byte Arena.

While your agent can be coded in whatever programming language you like, this section will show you to implement one in JavaScript.

# Prerequisite

- You have installed the [Byte Arena CLI](/doc/the-bytearena-cli).

- You have a running Docker daemon (please refer to [Docker's documentation](https://docs.docker.com/) to install it if not).

- You know JavaScript.

# Scaffolding your agent

`ba` is the name of the Byte Arena command line interface (CLI).

Use it to scaffold the code for your first agent.

```sh
$ ba generate nodejs
```

This command will generate a directory containing the nodejs source code of a basic agent.

Example:

<script type="text/javascript" data-rows="40" src="https://asciinema.org/a/N2YzvXPTWoZI4rBvdpu8LkfI2.js" id="asciicast-N2YzvXPTWoZI4rBvdpu8LkfI2" async></script>

In this example, a directory named `powerful-jennet` has been generated, and the code it contains built in a docker container under the same name.

# Giving it a ride

The agent you just built is already able to fly!

Try it with this command (replace `powerful-jennet` with the name of your agent):

<script type="text/javascript" data-rows="40" src="https://asciinema.org/a/JwmtBpH9wP9xNqSegw9UC6dhm.js" id="asciicast-JwmtBpH9wP9xNqSegw9UC6dhm" async></script>

A browser should open at http://localhost:8080/arena/1, displaying the Byte Arena visualization, where you'll find your agent.

> TODO:image here

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
