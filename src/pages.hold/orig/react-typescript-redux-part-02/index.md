---
title: Adding TypeScript (incrementally) to Create React App
date: '2019-04-03'
spoiler: Don't know yet
---

#5

In part 1 we used Create React App to create a basic React with TypeScript project. In this installment, we will be greatly expanding the project by adding and makeing use of:

- Ramda
- Redux
- classnames
- recompose
- redux-devtools-extension
- redux-thunk
- jss-preset-default
- @types/ramda
- @types/classnames


# Redux & redux-devtools-extension

> If you haven't yet, install Redux Devtools extension in Firefox and/or Chrome

```js
npm i -S redux react-redux redux-devtools-extension redux-thunk

npm i -D @types/react-redux
```

Change `src/index.tsx` to this:
```js
import * as React from 'react'
import { render } from 'react-dom'
import { Provider } from 'react-redux'
import configureStore from './redux'

import Wrapper from './App'
import './index.css'

const store = configureStore()

const renderApp = () =>
  render(
    <Provider store={store}>
      <Wrapper />
    </Provider>,
    document.getElementById('root')
  )

if (process.env.NODE_ENV !== 'production' && module.hot) {
  module.hot.accept('./ui/App', renderApp)
}

renderApp()

```

You'll notice that `.hot` is underlined. To solve this, add @types/webpack-env

```js
npm i -D @types/webpack-env
```

Since `src/index.tsx` is referencing `./redux` which does not exist yet, the project won't run. We solve this in the next section

# Adding the Redux store

> This section is largly from the Redux documentation

I don't think of actions, reducers & selectors as part of the *store*, so I name the folder that contains all the Redux files `redux`.

For the sake of learning and getting things working, let's setup a simple use of Redux to get things working before we get into using `redux-thunk` and the API/Rest Server.

The redux project structure will be

```js
cd src

mkdir redux

cd redux

touch index.js monitorReducer.js reduxLogger.js rootReducer.js


```

**index.js**
```js
import { applyMiddleware, compose, createStore } from "redux"
import thunkMiddleware from 'redux-thunk'
import { composeWithDevTools } from 'redux-devtools-extension'

import monitorReducerEnhancer from './monitorReducer'
import loggerMiddleware from './reduxLogger'
import { rootReducer } from './rootReducer'

export default function configureStore(){
  const middlewares = [/*loggerMiddleware,*/ thunkMiddleware]
  const middleWareEnhancer = applyMiddleware(...middlewares)

  const enhancers = [/*monitorReducerEnhancer*/]
  const composedEnhancers = compose(...enhancers)

  const store = createStore(
    rootReducer,
    composeWithDevTools(middleWareEnhancer, composedEnhancers)
  )

  if (process.env.NODE_ENV !== 'production' && module.hot) {
    module.hot.accept('./', () => store.replaceReducer(rootReducer))
  }

  return store
}

```

**monitorReducer.js**
```js
const round = number => Math.round(number * 100) / 100

const monitorReducerEnhancer = createStore => (
  reducer,
  initialState,
  enhancer
) => {
  const monitoredReducer = (state, action) => {
    const start = performance.now()
    const newState = reducer(state, action)
    const end = performance.now()
    const diff = round(end - start)

    console.log('reducer process time:', diff)

    return newState
  }

  return createStore(monitoredReducer, initialState, enhancer)
}

export default monitorReducerEnhancer

```

**reduxLogger.js**
```js
const logger = store => next => action => {
  console.group(action.type)
  console.info('dispatching', action)
  let result = next(action)
  console.log('next state', store.getState())
  console.groupEnd()
  return result
}

export default logger
```
**rootReducer.js**
```js
import { combineReducers } from "redux"
import { todosReducer } from './todo/reducers'
import { requestsReducer } from './requests/reducers'

export const rootReducer = combineReducers({
  todos: todosReducer,
  requests: requestsReducer
})
```


# Delete src/index.css

Delete the file src/index.tsx and remove its import from src/index.tsx

Because are using @global in Wrapper


