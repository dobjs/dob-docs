---
title: Observable
layout: guide
order: 1
---

`observable` use `proxy` to return a proxy object, the proxy object can be monitored by `observe`.

```typescript
import { observable } from "dob"
```

## Usage

```javascript
// es5
observable(obj)

// es6
@observable
class Obj {
    someField = ".."
}
```

## Features

`observable` support native `object`、`array`、`Map`、`WeakMap`、`Set`、`WeakSet`, support undefined variables, dynamic conditional branches.

### Object

```javascript
const obj = observable({
    user: {
        name: "jeck",
        age: 25,
    }
})
observe(() => {
    console.log(`${obj.user.name}, ${obj.user.age}`)
})
obj.user.name = "bob"
obj.user = {
    name: "well",
    age: 16,
}
delete obj.user.name
```

{% raw %}
<div id="demo-object" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
    const obj = observable({
        user: {
            name: "jeck",
            age: 25,
        }
    })
    observe(() => {
        log('#demo-object div', `${obj.user.name}, ${obj.user.age}`)
    })
    obj.user.name = "bob"
    obj.user = {
        name: "well",
        age: 16,
    }
    delete obj.user.name
})()
</script>
{% endraw %}

### Array

Only when the variables used are modified, the action will be triggered again.

```javascript
let arr = observable([1, 2, 3, 4, 5])
observe(() => {
    console.log(`${arr.map(i => i)}`)
})
arr[0] = 10
arr.push(6)
Action(()=>{ arr.shift() })
Action(()=>{ arr.splice(2, 1) })
delete arr[0]
```

{% raw %}
<div id="demo-array" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
    let arr = observable([1, 2, 3, 4, 5])
    observe(() => {
        log('#demo-array div', `${arr.map(i => i)}`)
    })
    arr[0] = 10
    arr.push(6)
    Action(()=>{ arr.shift() })
    Action(()=>{ arr.splice(2, 1) })
    delete arr[0]
})()
</script>
{% endraw %}

> Because of JS achieve `shift` `splice` by divided into multiple steps, so use `Action` can be aggregated into an action.

`.length` will trigger action when any change, which will change array's length:

```javascript
let arr = observable([1, 2, 3, 4, 5])
observe(() => {
    console.log(`${arr.length}`)
})
arr.push(6)
arr.splice(2, 1)
```

{% raw %}
<div id="demo-array-1" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
    let arr = observable([1, 2, 3, 4, 5])
    observe(() => {
        log('#demo-array-1 div', `${arr.length}`)
    })
    arr.push(6)
    arr.splice(2, 1)
})()
</script>
{% endraw %}

### Map

listen size:

```javascript
const map = observable(new Map())
observe(() => {
    console.log(`${map.size}`)
})
map.set("banana", 5)
map.set("apple", 3)
map.clear()
```

{% raw %}
<div id="demo-map" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
    const map = observable(new Map())
    observe(() => {
        log('#demo-map div', `${map.size}`)
    })
    map.set("banana", 5)
    map.set("apple", 3)
})()
</script>
{% endraw %}

listen single key:

```javascript
const map = observable(new Map())
observe(() => {
    console.log(`${map1.get("apple")}`)
})
map1.set("apple", 6)
```

{% raw %}
<div id="demo-map-1" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
    const map = observable(new Map())
    observe(() => {
        log('#demo-map-1 div', `${map.get("apple")}`)
    })
    map.set("apple", 6)
})()
</script>
{% endraw %}

### WeakMap

Same with Map.

### Set

listen size:

```javascript
const set = observable(new Set())
observe(() => {
    console.log(`${set.size}`)
})
set.add("banana")
set.add("apple")
set.clear()
```

{% raw %}
<div id="demo-set" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
    const set = observable(new Set())
    observe(() => {
        log('#demo-set div', `${set.size}`)
    })
    set.add("banana")
    set.add("apple")
    set.clear()
})()
</script>
{% endraw %}

### WeakSet

Same with Set.

### Expand thinking

All of the basic type as shown above can be used in object:

```javascript
const obj = observable({
    simpleNumber: 1,
    simpleString: "text~",
    simpleArray: [1, 2, 3, 4, 5],
    map: new Map([ ["a", 1], ["b", 2], ["c", 3] ]),
    deepObj: {
    	user: {
      	articles: [{
        	title: "nodejs"
        }]
      }
    },
    show: false
})
```

## Dynamic binding

For uninitialized variables, can also be tracked.

```typescript
const obj = observable({})
observe(() => {
    log('#demo-dynamic-binding div', `${obj.a}`)
})
obj.a = 3
```

{% raw %}
<div id="demo-dynamic-binding" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
    const obj = observable({})
    observe(() => {
        log('#demo-dynamic-binding div', `${obj.a}`)
    })
    obj.a = 3
})()
</script>
{% endraw %}

## Conditional branch

```typescript
const objCon = observable({
    useA: true,
    a: 1,
    b: 2
})

observe(() => {
    if (objCon.useA) {
        console.log(objCon.a) 
    }
})

objCon.a = 3
objCon.useA = false
objCon.a = 4 // not work
```

{% raw %}
<div id="demo-conditional-branch" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
    const obj = observable({
        useA: true,
        a: 1,
        b: 2
    })
    observe(() => {
        if (obj.useA) {
            log('#demo-conditional-branch div', `${obj.a}`)
        }
    })
    obj.a = 3
    obj.useA = false
    obj.a = 4 // not work
})()
</script>
{% endraw %}
