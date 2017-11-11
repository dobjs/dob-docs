---
title: IsObservable
layout: guide
---

`isObservable` is a method to check whether the object is an observable object.

```typescript
import { isObservable } from "dob"
```

## Usage

```javascript
isObservable(obj)
```

## Example

```javascript
const obj1 = {}
const obj2 = observable({})

console.log(isObservable(obj1), isObservable(obj2))
```

{% raw %}
<div id="demo-1" class="demo-after-code">
    <div class="result"></div>
</div>
<script>
(()=>{
  const obj1 = {}
  const obj2 = observable({})
  log('#demo-1 div', isObservable(obj1), isObservable(obj2))
})()
</script>
{% endraw %}