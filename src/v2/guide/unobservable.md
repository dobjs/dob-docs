---
title: unobserve
layout: guide
---

stop observe.

## Usage

```javascript
const obj = observable({
    text: "init"
})

const signal = observe(() => {
    console.log('dynamicObj.a')
})

signal.unobserve()
```

{% raw %}
<div id="demo-one" class="demo-after-code">
    <button onclick="stopObserve()">stop observe</button>
    <input type="text" placeholder="change text" oninput="changeText(this.value)"></input>
    <div class="result"></div>
</div>
<script>
const obj = observable({
    text: "init"
})
const signal = observe(() => {
    document.querySelector('#demo-one div').innerHTML = `${obj.text}`
})
function changeText(value){
    obj.text = value    
}
function stopObserve(){
    signal.unobserve()
}
</script>
{% endraw %}