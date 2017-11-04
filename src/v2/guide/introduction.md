---
title: Introduction
layout: guide
order: 0
---

<img src="https://avatars1.githubusercontent.com/u/32093464?s=200&v=4" width=100 />

[dob](https://github.com/dobjs/dob) is a tool for monitoring object changes by using Proxy.

```typescript
import { observable, observe } from "dob"

// 1. Create an observabled obj
const obj = observable({ a: 1 })

// 2. Observe obj.a
observe(() => {
    console.log("obj.a has changed to", obj.a)
})

// 3. Change obj.a, and observe's callback will execute
obj.a = 2 
```

## Using dob with react

[dob-react](https://github.com/dobjs/dob-react) can bind dob to React, read [QuickStart](quick-start.html) for more information.

> [dob-react-devtools](https://github.com/dobjs/dob-react-devtools) is a good library to help you debug code written by `dob`.

## Using both dob and redux

If you want to use functional development, as well as redux-devtools, but tired of immutable tedious usage, you can now use mutable methods to replace immutable wording.

[dob-redux](https://github.com/dobjs/dob-redux) can bind dob to Redux. You can keep using react-redux and all the redux ecology.

> If `dob-react` is used, there is no need to use `dob-redux`, it's only offered as another development idea.
