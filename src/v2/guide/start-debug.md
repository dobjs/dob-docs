---
title: StartDebug
layout: guide
---

Start debug, so you can listen `debug` by using `dobEvent`. THis is a low level api.

## Usage

```javascript
import { startDebug, dobEvent } from "dob"

startDebug()

dobEvent.on("debug", debugInfo => {
  console.log(debugInfo)
})
```

## StopDebug

```javascript
import { stopDebug } from "dob"

stopDebug()
```

> The most common use is [debug in dob-react](./devtools.html)

## Defintion

`IDebugInfo`:

```typescript
interface IDebugInfo {
  /**
   * uniqueId, you can also receive it from `observe` or `reaction` callback first argument's field `debugId`
   */
  id?: number
  /**
   * action's name
   */
  name?: string
  type: string
  changeList?: Array<{
    type: string
    /**
     * called child action in this action, when type is action
     */
    action?: IDebugInfo
    callStack: PropertyKey[]
    oldValue?: any
    /**
     * new value
     */
    value?: any
    /**
     * operate key
     */
    key?: PropertyKey
    customMessage?: any[]
  }>
}
```