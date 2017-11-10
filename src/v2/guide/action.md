---
title: Action
layout: guide
order: 2
---

`Action` is to reduce the number of dependency tracking triggers, it can collect all changes, and then merge trigger.

```typescript
import { Action } from "dob"
```

## Features

```typescript
import { observe, observable, Action } from 'dob'

const obj = observable({
    a: 1
})

observe(() => {
    console.log('dynamicObj.a change to', obj.a)
})

Action(()=> {
    obj.a = 2
    obj.a = 3
    obj.a = 4
    obj.a = 5
})
```

{% raw %}
<div id="demo-one" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
    const obj = observable({
     a: 1
    })
    observe(() => {
        log("#demo-one > div", obj.a)
    })
    Action(()=> {
        obj.a = 2
        obj.a = 3
        obj.a = 4
        obj.a = 5
    })
})()
</script>
{% endraw %}

There are three changes can be seen merged.

## ESNext usage

```typescript
@Action someAction() {
    obj.a = 2
    obj.a = 3
}
```

## In StrictMode

Changes only allowed run in `Action` in the `strictMode`.

**note**: `async` `await` seems like synchronization, in fact, is asynchronous, so it's necessary to pay attention to the following wording:

```javascript
@Action async someAction() {
    this.store.isLoading = true
    const result = await fetch("..")
    Action(()=>{
        this.store.isLoading = false
        this.store.result = result
    })
}
```

the code after `await` row, will be in a separate stack to run, that is, not in the current Action. 