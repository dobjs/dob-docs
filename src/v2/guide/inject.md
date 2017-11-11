---
title: Inject
layout: guide
---

`inject` any class, which both created by `combineStore`.

```typescript
import { inject, combineStore } from "dob"
```

## Usage

```javascript
class A {
  value = 5
}

class B {
  @inject(A) a

  showValue() {
    return this.a.value
  }
}

const stores = combineStore({A, B})

console.log(stores.B.showValue()) // 5
stores.A.value = 6
console.log(stores.B.showValue()) // 6
```
