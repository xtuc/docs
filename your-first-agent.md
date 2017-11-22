---
title:  Create your first agent
author: Sven Sauleau
date:   2017-11-16
include_js:
    - https://cdnjs.cloudflare.com/ajax/libs/prism/1.8.4/components/prism-docker.min.js
content: |
    We will be going through the implementation of a basic agent in JavaScript.

    # Prerequisite

    - This article assumes you already know how to develop a program in JavaScript.
    - You need a running Docker daemon, please refer to [Docker's documentation](https://docs.docker.com/) to install it.

    # Getting started

    ```sh
    $ ba generate nodejs
    ```

    The agent will be located in the current directory.

    # Connection to the game server

    Here is a boilersplate to etablish the connection to the game server:

    ```js
    import {comm} from 'bytearena-sdk';

    const agent = comm.connect();
    ```

    At this point you can already launch the trainer with your agent.

    # Building your agent

    In the root directory of your program, run the following command:

    ```sh
    $ ba build [AGENT_DIRNAME]
    ```

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

    # Interpreting the perception

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
