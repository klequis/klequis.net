---
title: Adding TypeScript to Create React App
date: '2019-03-12'
spoiler: I didn't find the doc to tell the whole story and I wanted to go beyond the basic implementation to something more like my non-TypeScript starter template.
---

This is my first full post with the new blog platform and things need some help.

After following the [directions for adding TypeScript to Create React App](https://reactjs.org/docs/static-type-checking.html#adding-typescript-to-a-project) there seemed room for improvement. I got some initial errors. I also wanted to add some things that I'm used to using when working on non-TypeScript projects. The below is notes on my journey, somewhat organized like a tutorial, but not fully vetted as such yet (today 12-Mar-19).

> It seems odd that Create React App puts dev dependencies in 'depenencies' and not 'devDependencies' in package.json. For an explanation see [comment by gaearon](https://github.com/facebook/create-react-app/issues/1764#issuecomment-285082921)

Not sure if I did something wrong but I got over 30 warnings when using Yarn to add TypeScript and related type definitions my project. Most worrisome of them was a message about packages being removed because they were not installed by me. Since I generally use [npm]() anyway, I switched to npm and got no warnings.
- This same error happens if you use npm immediately following npx create-react-app --typescript. To get around this, delete both /node_modules and yarn.lock before running any npm commands.

The below is from Create React App [documentation](https://facebook.github.io/create-react-app/docs/adding-typescript), except that it deletes yarn.lock & node_modules and reinstalls using npm.

## Create the app
```js
npx create-react-app adding-typescript --typescript
```

Swith out Yarn for npm
```js
rm yarn.lock
rm -rf node_modules
npm i
```

## commit changes
```js
git add .
git commit -m 'switch to npm'
```

## install TypeScript and related type definitions
```js
npm install --save typescript @types/node @types/react @types/react-dom @types/jest
```

## Rename src/index.js to src/index.tsx
```js
cd src
mv index.js index.tsx
```
## commit changes
```js
git add .
git commit -m 'typescript added'
```

## Run it
```js
npm start
```

## Commit changes
Running the app added a couple of files
```js
git add .
git commit -m 'after first run'
```

## Eject
```js
// from project root
npm run eject
```

## Commit changes

```js
git add .
git commit -m 'after eject'
```

## Examine differences in package.json
@types/enzyme
@types/enzyme-adapter-react-16

babel - cra is using @babel/core": "7.2.2" with babel-core": "7.0.0-bridge.0 (leave as is)

enzyme
enzyme-adapter-react-16
jest-environment-enzyme
jest-enzyme

under "jest"
> cra is using "testEnvironment": "jsdom"
"setupTestFrameworkScriptFile": "jest-enzyme",
"testEnvironment": "enzyme",
"testEnvironmentOptions": {
  "enzymeAdapter": "react16"
},


## tsconfig.json differences
| field | starter | cra |
| ----- | ------- | --- |
| jsx | react | preserve |
| lib | dom, es6 | esnext, dom, dom.iterable |
| skipLibCheck | n/a | true |
| allowSyntheticDefaultImports | n/a | true |
| resolveJsonModule | n/a | true |
| isolatedModules | n/a | true |
| noEmit | n/a | true |
| include | n/a | src |
| baseUrl | src | n/a |
| outDir | build/dist | n/a |
| sourceMap | true | n/a |
| rootDir | src | n/a |
| noImplicitReturns | true | n/a |
| noImplicitThis | true | n/a |
| noImplicitAny | true | n/a |
| importHelpers | true | n/a |
| strictNullChecks | true | n/a |
| suppressImplicitAnyIndexErrors | true | n/a |
| noUnusedLocals | true | n/a |



## Commit changes due to comparison
**no actual change**
```js
git add .
git commit -m 'reordered tsconfig'
```

## Rename UI files
In TypeScript
- files with jsx files are .tsx
- regular .js files are .ts

```js
cd src
mv App.js App.tsx
mv App.test.js App.test.tsx
```

## Current project structure
<picture Selection_04g>

## Run it
```js
npm start
```

## Run tests
```js
npm test
```
<picture Selection_046>

## Reorg project structure
The current structure from Create React App is good for a quick example, but something a bit different is needed for a larger project.
I'm making these changes in a file manager
1. create directory /src/ui - this will be used for all unique UI components
1. create directory /src/ui/App - yes, capital 'A'
1. move App.css, App.test.tsx, App.tsx & logo.svg to /src/ui
1. create file /src/ui/App/index.ts
```js
export { default } from './App'
```
1. modify src/index.ts
```js
- import App from './App'
+ import App from './ui/App'
```

TypeScript also uses [Type assertions](https://github.com/Microsoft/TypeScript-React-Starter#type-assertions). Modify index.ts to be
```js
ReactDOM.render(
  <App />,
  document.getElementById('root') as HTMLElement
);
```
See [Type assertions](https://github.com/Microsoft/TypeScript-React-Starter#type-assertions) for why.

1. while here, if you don't intend to use the service worker remove it and delete src/serviceWorker.js




## Run tests then app to make sure all is good
```js
npm test
npm start
```



## New Structure
<picture Selection_047.png>


## Using absolute imports for components
Create another component and import it with an absolute reference
1. create folder src/ui/Hello
1. in Hello create files Hello.tsx & index.ts

```js
// Hello.tsx

import React from 'react'

const Hello = () => {
  return <h1>Hello</h1>
}

export default Hello
```

```js
// index.ts
export { default } from './Hello'
```

Modify
```js
// App.tsx

import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
+ import Hello from '../Hello'

class App extends Component {
  render() {
    return (
      <div className="App">
        <header className="App-header">
+         <Hello />
          <img src={logo} className="App-logo" alt="logo" />
          <p>
            Edit <code>src/App.js</code> and save to reload.
          </p>
          <a
            className="App-link"
            href="https://reactjs.org"
            target="_blank"
            rel="noopener noreferrer"
          >
            Learn React
          </a>
        </header>
      </div>
    );
  }
}

export default App;

```

```js
npm start
```

This gives a surprising error
```js
TypeScript error: Cannot compile namespaces when the '--isolatedModules' flag is provided.  TS1208
```
The cure is to rename Hello/index.ts to index.tsx





# Extra
"exclude": [
    "src/serviceWorker.js"
  ]

## Resources

- https://piotrwitek.github.io/react-redux-typescript-guide/#fcspreadattributes