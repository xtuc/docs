---
title:  Handshake specification
include_js:
  - https://cdnjs.cloudflare.com/ajax/libs/prism/1.8.4/components/prism-go.min.js
---

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
