---
title: Connect
layout: guide
---

`Connect` store and action to react component.

## Simple Usage

```typescript
import { Provider, Connect } from 'dob-react'

@Connect
class App extends React.Component <any, any> {
    render() {
        return (
            <span>{this.props.store.name}</span>
        )
    }
}

ReactDOM.render(
    <Provider store={{ name: 'bob' }}>
        <App />
    </Provider>
, document.getElementById('react-dom'))
```

`Connect`: All parameters from outer Provider are injected into the wrapped components, and the component rerender when the variables used in the render function are modified(sync usage).

## `Connect` all functions

### Connect all

Connect all from Provider's parameters, also is this example above.

### Connect extra data

> Will also inject all parameters from outer Provider.

```typescript
@Connect({
    customStore: {
        name: 'lucy'
    }
})
class App extends React.Component <any, any> {}
```

### Map state to props

> Will also inject all parameters from outer Provider.

```typescript
@Connect(state => {
    return {
        customName: 'custom' + state.store.name
    }
})
class App extends React.Component <any, any> {}

ReactDOM.render(
    <Provider store={{ name: 'bob' }}> <App /> </Provider>
, document.getElementById('react-dom'))
```

### Support stateless component

```typescript
class App extends React.Component <any, any> {
    render() {
        return (
            <span>{this.props.store.name}</span>
        )
    }
}

const ConnectApp = Connect()(App)
// const ConnectApp = Connect({ ... })(App)
// const ConnectApp = Connect( state => { ... })(App)
```