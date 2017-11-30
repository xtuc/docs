---
title:  The container of your agent
include_js:
    - https://cdnjs.cloudflare.com/ajax/libs/prism/1.8.4/components/prism-docker.min.js
---

A `Dockerfile` file is required at the root of your project in order to create your container and to deploy your agent.

# Sample Node.js Dockerfile

Imagine you want to bundle your existing Node.js program.

Here is an example using the official Node.js (version 7) image:

```docker
FROM node:7

WORKDIR /usr/app

# Install app dependencies
COPY package.json /usr/app/
RUN npm install

# Bundle app source
COPY . /usr/app

CMD [ "npm", "start" ]
```
You are free to take any version available on the Docker hub ([see available Docker images](https://hub.docker.com/_/node/)).

# Connecting to our game server

We are going to inject a few environement variables into your container, you can then use them in the entrypoint of your container:
- `PORT`: the game server port
- `HOST`: the game server host
- `AGENTID`: the identifier of your agent in the game (needed in our communication protocol)

# Security

## Network

Your network is restricted, you won't be able to reach the outside or communicate directly with other agents.

You are only authorized to communicate with the game server.

## Forbidden intructions

For security reason, you can only use the following instructions in your Dockerfile:
    - `COPY`
    - `ENV`
    - `FROM`
    - `RUN`
    - `CMD`
    - `ENTRYPOINT`
    - `WORKDIR`

The push on our Git server will be forbidden if you use other instructions.

## File system

The container uses a read-only filesystem.

## Capabilities

All Unix Capabilities are dropped and your container is not privileged.

## Unix user

You are not allowed to change the Unix user or group which will execute your program.

The user `nobody` must be present in the container in order to run your program. Note that most Linux distribution have it.
