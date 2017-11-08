---
title: For react
layout: guide
---

Follow the steps below to use dob in react:

Create store and action -> `combineStores` -> `Provider` -> `Connect` in component, and use all store&action

![stores](https://camo.githubusercontent.com/12bad0e0f215b60f578f27e5c3c3c01ea8ad5f05/68747470733a2f2f696d672e616c6963646e2e636f6d2f7466732f544231657050506d6a6968534b4a6a793046655858624a747058612d3638372d3433352e706e67)

## Create store and action

For example, we create `ArticleStore` and `ArticleAction` to manage articles.

**`@inject` will inject single same instance into any instance, which generated using `combineStore`. **

```typescript
import { observable, inject, Action } from "dob"
import { Provider, Connect } from "dob-react"

@observable
class ArticleStore {
  articles = []
}

class ArticleAction {
  @inject(ArticleStore) articleStore

  @Action addArticle() {
    this.articleStore.articles.push({ title: "new Article" })
  }
}
```

## Combine all of the actions and stores

As the above example shows, we combine `ArticleStore` and `ArticleAction` using `combineStores`.

**`combineStores` will create single instance for each actions and stores, and help `@inject` take effect.**

```typescript
import { combineStores } from "dob"

export const allStores = combineStores({
    ArticleStore,
    ArticleAction
})
```

## Use Provider in react root node

use `Provider` in the root node, it's an important step to inject stores to all child component.

**`Provider` will inject all the parameters it receives into the components that use the `Connect`**.

```typescript
import { Provider } from "dob-react"

ReactDOM.render(
    <Provider {...allStores}>
        <App />
    </Provider>
, domNode)
```

## Use Connect in react component

finally, you can use all Actions and Stores in any react component that use `Connect`.

**`@Connect` has two functions:**

**1. Pass all stores and actions to current component's props, which registered in `Provider`.**
**2. Auto rerender current component, when the store data it uses changed.**

```typescript
import { Connect } from "dob-react"

@Connect
class App extends React.Component {
    render() {
        return (
            <span
              onClick={() => {
                this.props.ArticleAction.addArticle()
              }}
            >Article count: {this.props.ArticleStore.articles.length}</span>
        )
    }
}
```

That's all.