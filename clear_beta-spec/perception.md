---
title:  Perception specification
author: Sven Sauleau
date:   2017-11-28
include_js:
  - https://cdnjs.cloudflare.com/ajax/libs/prism/1.8.4/components/prism-go.min.js
---

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
