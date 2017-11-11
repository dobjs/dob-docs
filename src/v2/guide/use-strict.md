---
title: UseStrict
layout: guide
---

`useStrict` is a method to open strict mode in dob.

```typescript
import { useStrict } from "dob"
```

## Usage

```javascript
useStrict()
```

## Strict Mode

It's not allow to change any observable value out of `Action`:

```javascript
useStrict()

const obj = observable()
obj.title = "bob" // throw error!

Action(() => {
  obj.title = "bob" // it's ok!
})
```

## ESNext Usage

`Action` with decorator usage.

```javascript
useStrict()

class SomeStore {}

class SomeAction {
  @inject(SomeStore) store

  @Action methodTwo() {
    this.store.title = "bob" // it's ok!
  }
}
```

## cancelStrict

To cancle strict mode.

```javascript
import { cancelStrict } from "dob"
cancelStrict()
```