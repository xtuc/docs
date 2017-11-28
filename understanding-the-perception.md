---
title:  Understanding the perception
author: Sven Sauleau
date:   2017-11-16
include_js:
  - https://cdnjs.cloudflare.com/ajax/libs/prism/1.8.4/components/prism-go.min.js
---

# Perception representation

The following specification is only for the `clear_beta` protocol version. Make sure you are using it before continuing to read.

**This specification is subject to changes.**

## Types in JSON

- `Vector2`: an array of the shape `[x, y]` where `x` and `y` are of type `float64`.
- `Angle`: a `float64` representing a radian.
- `ItemTag`: the possible values are `agent`, `obstacle` and `projectile`.

## Handshake structure

After the handshake some data will be send back to the agent, with the following properties:

```go
/*
    This object is the specifications of your agent.
*/
type specs struct {

    // max distance covered per turn
    maxspeed           float64

    // max force applied when steering (ie, max magnitude of steering vector)
    maxsteeringforce   float64

    // ^ same when chaning directions
    maxangularvelocity float64

    // Distance of vision
    visionradius       float64

    // Angle of vision
    visionangle        Angle

    bodyradius         float64

    /*
       Force against the agent.
       It's used to represent all the physical constraints related to the environment.

       You can calculate your position at the next tick using the following formula, given that `x` is the steering you want and `x` < `maxsteeringforce`:

       x' = x - dragforce 
    */
    dragforce          float64

}
```

## Perception structure

The root object is called `perception`, it's the object you receive in argument in the `onTick` function.


```go
type perception struct {

      /*
          Description of every objects that the agent can see.
      */
      vision []struct {

          // Item identification
          tag      ItemTag

          nearedge Vector2
          center   Vector2
          faredge  Vector2
          velocity Vector2
      }

      energy           float64

      // Angle to the north
      azimuth          float64

      // Velocity of the item (if any)
      velocity         Vector2

      // Radius of the body of the item (if any)
      bodyradius       float64
}
```

All the points are expressed using a vector relative to the agent.

### World

![world](/assets/img/perception-world.svg)

### Item in the vision

#### Obstacles

Obstacle are static items, I omited the vector because it is equal to null.

![perception](/assets/img/perception-object-cross.svg)

In this example, you can see two faces of the object. They share the same vector to the `nearedge`. The other points are not given since they are not visible from the agent point of view.

#### Projectiles and agents

Projectiles and agents (unlike obstacles) are perceived as circles with a velocity (the blue arrow).

![perception2](/assets/img/perception-agent.svg)
