---
title:  Perception specification
include_js:
  - https://cdnjs.cloudflare.com/ajax/libs/prism/1.8.4/components/prism-go.min.js
---

## Perception structure

The root object is called `perception`, it's the object you receive in argument in the `onTick` function.

<a name="agentPerception"></a>
### `agentPerception`

| Property name | Type | Representation in the JSON |
|---|---|
| score | `int` | `Number` |
| energy | `float64` | `Number` |
| velocity | `vector.Vector2` | `Array of x, y` |
| azimuth | `float64` | `Number` |
| vision | `array agentPerceptionVisionItem` | `Array of Object` |
| shootenergy | `float64` | `Number` |
| shootcooldown | `int` | `Number` |
| messages | `array mailboxMessagePerceptionWrapper` | `Array of Object` |


<a name="agentPerceptionVisionItem"></a>
### `agentPerceptionVisionItem`

| Property name | Type | Representation in the JSON |
|---|---|
| tag | `string` | `String` |
| nearedge | `vector.Vector2` | `Array of x, y` |
| center | `vector.Vector2` | `Array of x, y` |
| faredge | `vector.Vector2` | `Array of x, y` |
| velocity | `vector.Vector2` | `Array of x, y` |


<a name="mailboxMessagePerceptionWrapper"></a>
### `mailboxMessagePerceptionWrapper`

| Property name | Type | Representation in the JSON |
|---|---|
| subject | `string` | `String` |
| body | `unknown` | `Object` |


<a name="Score"></a>
### `Score`

| Property name | Type | Representation in the JSON |
|---|---|
| value | `int` | `Number` |


<a name="Stats"></a>
### `Stats`

| Property name | Type | Representation in the JSON |
|---|---|
| distanceTravelled | `float64` | `Number` |


<a name="YouAreRespawning"></a>
### `YouAreRespawning`

| Property name | Type | Representation in the JSON |
|---|---|
| respawningin | `int` | `Number` |


<a name="YouHaveBeenFragged"></a>
### `YouHaveBeenFragged`

| Property name | Type | Representation in the JSON |
|---|---|
| by | `string` | `String` |


<a name="YouHaveBeenHit"></a>
### `YouHaveBeenHit`

| Property name | Type | Representation in the JSON |
|---|---|
| kind | `string` | `String` |
| comingfrom | `float64` | `Number` |
| damage | `float64` | `Number` |


<a name="YouHaveFragged"></a>
### `YouHaveFragged`

| Property name | Type | Representation in the JSON |
|---|---|
| who | `string` | `String` |


<a name="YouHaveHit"></a>
### `YouHaveHit`

| Property name | Type | Representation in the JSON |
|---|---|
| Who | `string` | `String` |


<a name="YouHaveRespawned"></a>
### `YouHaveRespawned`

