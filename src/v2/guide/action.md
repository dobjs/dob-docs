---
title: Action
layout: guide
order: 2
---

`Action` is to reduce the number of dependency tracking triggers, it can collect all changes, and then merge trigger.

```typescript
import { Action } from "dob"
```

## ES5 usage

```typescript
import { observe, observable, Action } from 'dob'

const dynamicObj = observable({
    a: 1
})

observe(() => {
    console.log('dynamicObj.a change to', dynamicObj.a)
})

Action(()=> {
    dynamicObj.a = 2
    dynamicObj.a = 3
})
```

The above will output two messages:

`dynamicObj.a change to 1`
`dynamicObj.a change to 3`


There are two changes can be seen merged.

## ES6 usage

```typescript
import { observe, observable, Action } from 'dob'

const dynamicObj = observable({
    a: 1
})

observe(() => {
    console.log('dynamicObj.a change to', dynamicObj.a)
})

class CustomAction {
    @Action someAction() {
        dynamicObj.a = 2
        dynamicObj.a = 3
    }
}

new CustomAction().someAction()
```

The same effect:

`dynamicObj.a change to 1`
`dynamicObj.a change to 3`