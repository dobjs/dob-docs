---
title: Introduction
layout: guide
order: 0
---

<a href="https://github.com/dobjs/dob" target="_blank">
    <img src="https://avatars1.githubusercontent.com/u/32093464?s=200&v=4" width=100 />
</a>

[dob](https://github.com/dobjs/dob) is a tool for monitoring object changes by using Proxy.

[![CircleCI Status](https://img.shields.io/travis/dobjs/dob/master.svg?style=flat)](https://travis-ci.org/dobjs/dob) [![npm version](https://img.shields.io/npm/v/dob.svg?style=flat)](https://www.npmjs.com/package/dob) [![code coverage](https://img.shields.io/codecov/c/github/dobjs/dob/master.svg)](https://codecov.io/github/dobjs/dob)

![npm](https://nodei.co/npm/dob.png?downloadRank=true&downloads=true)

```typescript
import { observable, observe } from "dob"

// 1. Create an observabled obj, and store runCount
const obj = observable({ })
let runCount = 0

// 2. Observe obj.text
observe(() => {
    runCount++
    document.write(`text: ${obj.text} & runCount: ${runCount}`)
})

// 3. Change obj.text, and observe's callback will execute
function changeText(value) {
    obj.text = value
}

// 4. Change obj.name, but step 2 not use it, so nothing happened
function changeName(value) {
    obj.name = value
}
```

{% raw %}
<div id="demo-1" class="demo-after-code">
    <input type="text" placeholder="change text" oninput="changeText(this.value)"></input>
    <input type="text" placeholder="change name" oninput="changeName(this.value)"></input>
    <div class="result"></div>
</div>
<script>
const obj = observable({ })
let runCount = 0
observe(() => {
    runCount++
    document.querySelector('#demo-1 div').innerHTML = `text: ${obj.text} & runCount: ${runCount}`
})
function changeText(value) {
    obj.text = value
}
function changeName(value) {
    obj.name = value
}
</script>
{% endraw %}


Look at the above results, if the changed field `obj.text` is used in the `observer`'s callback, change it will re-execute this function, but `obj.name` is not used, so it will not re-execute when change it.

> As you can see, even if you modify a property without a preset value, it still works.

## Using dob with react

[dob-react](https://github.com/dobjs/dob-react) can bind dob to React, read [For react](for-react.html) for more information.

> [dob-react-devtools](https://github.com/dobjs/dob-react-devtools) is a good library to help you debug code written by `dob`.

## Using both dob and redux

If you want to use functional development, as well as redux-devtools, but tired of immutable tedious usage, you can now use mutable methods to replace immutable wording.

[dob-redux](https://github.com/dobjs/dob-redux) can bind dob to Redux. You can keep using react-redux and all the redux ecology.

> If `dob-react` is used, there is no need to use `dob-redux`, it's only offered as another development idea.
