---
title: Quick start
layout: guide
order: 1
---

Data flow is shown in the diagram:

![stores](https://camo.githubusercontent.com/12bad0e0f215b60f578f27e5c3c3c01ea8ad5f05/68747470733a2f2f696d672e616c6963646e2e636f6d2f7466732f544231657050506d6a6968534b4a6a793046655858624a747058612d3638372d3433352e706e67)

First, create `ArticleStore` and `ArticleAction` with `dob`:

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

Special for `@inject` usage, it will inject single instance into any class, if you take all of them into `combineStores`:

```typescript
import { combineStores } from "dob"

export const allStores = combineStores({
    ArticleStore,
    ArticleAction
})
```

Then, use `Provider` in the root node:

```typescript
import { Provider } from "dob-react"

ReactDOM.render(
    <Provider {...allStores}>
        <App />
    </Provider>
, domNode)
```

`Provider` **inject all the parameters it receives into the components that use the `Connect`**, finally, you can use all Actions and Stores in any react component:

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
