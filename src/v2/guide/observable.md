---
title: Observable
layout: guide
order: 1
---

`observable` use `proxy` to return a proxy object, the proxy object can be monitored by `observe`.

```typescript
import { observable } from "dob"
```

## Features

`observable` support native `object`、`array`、`Map`、`WeakMap`、`Set`、`WeakSet`, support undefined variables, dynamic conditional branches.

Below is the details:

| Type | Description |
| -------- | -------- |
| object     | any |
| array | 支持单值访问、push splice pop unshift map foreach reduce 等操作的依赖追踪 |
| Map | 支持 has, get, forEach, keys, values, entries, delete, clear，以及 value 为任意嵌套对象的依赖追踪 |
| WeakMap | 支持 has, delete，以及 value 为任意嵌套对象的依赖追踪 |
| Set | 支持 has, forEach, keys, values, entries, delete, clear，以及 value 为任意嵌套对象的依赖追踪 |
| WeakSet | 支持 has, delete，以及 value 为任意嵌套对象的依赖追踪 |

## Dynamic binding

For uninitialized variables, you can also rely on tracking:

```typescript
import { observable, observe } from "dob"

const dynamicObj = observable({})

observe(() => {
    console.log("dynamicObj.a has changed to", dynamicObj.a) 
})

dynamicObj.a = 1
```


## Conditional branch

```typescript
import { observable, observe } from "dob"

const dynamicObj = observable({
    a: true,
    b: 1,
    c: 2
})

observe(() => {
    console.log("run")

    if (dynamicObj.a) {
        value = dynamicObj.b
    } else {
        value = dynamicObj.c
    }
})

dynamicObj.a = false
dynamicObj.b = 3
```
