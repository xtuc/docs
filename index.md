---
title:  Byte Arena
---

# What is Byte Arena?

Byte Arena is a gaming platform where you don't play, but let a virtual robot (we call it an agent) play for you.

Your task is to code the brain of the agent; we provide the bot, you provide the brain.

## What's an agent?

An agent is a piece of code that you write, that runs in a Docker container, and is able to communicate with the Byte Arena gaming platform using a simple and well defined API.

An agent perceives its digital environment, makes decisions, and takes actions to reach its objectives. Tweak it, evolve it, refine it, script it, make it learn — whatever works; one goal : overcome the opponents with your code.

## Can I see my agent?

Once your agent is coded, you can see in play against other players agents in your browser, evolving in a 3D world.

<video controls="controls" muted>
    <source type="video/mp4" src="https://s3.eu-central-1.amazonaws.com/bytearena-public/hexagon60.mp4"></source>
    <p>Your browser does not support the video element.</p>
</video>

## How is this even a game?

We find it's both stimulating and fun to make things and learn new stuff in the process, while challenging other players doing so; we hope you do too.

# The beta and its limitations

Byte Arena is not finished yet. We're currently on a beta version of things.

Ultimately, you'll be able to push your agents on [bytearena.com](https://bytearena.com) to compete with other players.

During beta, the online platform will not be available; [however, you can still train, debug and run your agents on your own computer using a simple command line tool we provide](the-bytearena-cli).

# Getting started

- [Create your container](agent-container)
- [The Bytearena CLI](the-bytearena-cli)

## Using JavaScript

While your agent can be coded in whatever programming language you like, this section will teach you to implement one in JavaScript.

- [Create your first agent](your-first-agent)
    - [Connect to the game server](your-first-agent#comm)
    - [Build your agent](your-first-agent#build)
    - [Taking actions](your-first-agent#take-actions)
    - [Receiving the environment](your-first-agent#perception)

# Platform specification

- [Understanding the perception](understanding-the-perception)

- API (`clear_beta` version)
    - [Handshake protocol](clear_beta-spec/handshake)
    - [Perception](clear_beta-spec/perception)
      - [Messages](clear_beta-spec/perception#messages)

# Community materials

- Articles
    - [Movement physics with vectors](https://www.xtuc.fr/notes/movement-physics-w-vectors.html)

- SDKs
    - [johnsudaar/go-bytearena](https://github.com/johnsudaar/go-bytearena)

# Further reading

- Videos
    - [Understanding vectors - The coding train](https://youtu.be/mWJkvxQXIa8)
    - [Autonomous agents and steering behavious - The coding train](https://youtu.be/JIz2L4tn5kM)

# Asking for help

If you encounter any problem or have a question, feel free to open an issue on either [ByteArena/cli](https://github.com/ByteArena/cli/issues) (for the CLI) or [ByteArena/community](https://github.com/ByteArena/community/issues) for any other topic.

Alternatively you can drop us a line at [hello@bytearena.com](mailto:hello@bytearena.com).

We are [@byte_arena](https://twitter.com/byte_arena) on Twitter.

We also have a Slack chat at https://bytearena.slack.com; ask us [on Twitter](https://twitter.com/byte_arena) for an invite.
