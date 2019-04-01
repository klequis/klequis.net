---
title: Adding TypeScript (incrementally) to Create React App
date: '2019-04-01'
spoiler: Don't know yet
---

> This isn't go to go well

> __April fools__


<hr/>

**ERROR: Property 'hot' does not exist on type 'NodeModule'.**

- Add @types/webpack-env

<hr/>


<hr>

**ERror Could not find a required file.**
  **Name: index.tsx**
  **Searched in: /home/klequis/dev/ts/todo.me/client.ts/src**

- Rename src/index.js to src/index.tsx
<hr>

## Convert App.js to App.tsx

<hr>

**Error**

**/home/klequis/dev/ts/todo.me/client.ts/src/ui/App/App.tsx**

**(2,21): Cannot find module 'ui/AddTodo'.**

- Renamed /src/AddTodo/index.js & /src/App/index.js to have .tsx extension.
  - this made no difference

- **Solution** is in tsconfig.json, change
`"baseUrl": "."` to `"baseUrl": "src"`

<hr>

## Convert `src/TodoList/TodosContainer.js` to .tsx

After renameing and restarting the first error is

`
/home/klequis/dev/ts/todo.me/client.ts/src/ui/TodoList/TodosContainer.tsx`

`(10,16): Property 'todosReadRequest' does not exist on type 'Readonly<{}> & Readonly<{ children?: ReactNode; }>'.
`

However, in `TodosContainer.tsx` 'todosReadRequest()', 'todos' and 'state' all have the red squiggly underline.

<hr>

**Parameter 'state' implicitly has an 'any' type.ts(7006)**

- Change `state` to `state: any`

<hr>

**Property 'todosReadRequest' does not exist on type 'Readonly<{}> & Readonly<{ children?: ReactNode; }>'.ts(2339)**

Add

```js
interface IProps {
  todos: []
  todosReadRequest: () => void
}
```

Which says that `todos` is an array & `todosReadRequest` is a function. However, there is likely a better/more exact way to type them.

Change

```js
class TodoContainer extends React.Component {
```

to

```js
class TodoContainer extends React.Component<IProps, []> {
```

<hr/>

## Convert /src/TodoList/Todo.js to .jsx

<img src='convert-Todo.js.png' alt='showing code module'>

<hr>

<img src='import-react-error.png' src='import react error'>

Solution is to change

```js
import React from 'react'
```
to
```js
import * as React from 'react
```

<img src='todo-has-implicit-any.png' alt='todo has implicit any error'>

- Add file `src/global-types.ts`
- Add a type for Todo
```js
export type Todo = {
  _id: string,
  title: string,
  completed?: boolean,
}
```
- In src/Todo.tsx
```js
import { Todo } from 'global-types'
```
And then change ...
```js
const Todo = ({ todo }) => {
```
to
```js
const Todo = ({ todo }: { todo: Todo }) => {
```


<hr>

<img src='classnames-error.png', alt='classnames error'>

Solution is

```
npm i -S classnames
npm i -D @types/classnames
```

<hr>

## Convert Todos.js to .tsx

Oddly, there were not errors highlighted in the code.

<img src='Todos.tsx.png', alt='Todos.tsx code' >

But there was one in the console

<img src='Todos.tsx.console-error.png' alt='Todos.tsx error in console'>