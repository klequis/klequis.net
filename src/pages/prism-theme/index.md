---
title: PrismJS Theme
date: '2019-03-14'
spoiler: Documentation of my Gatsby blog setup for PRISM syntax highlighting.
---

This article is more documentation and links on using PRISM with Gatsby and not intended as a how-to.


This blog is using [PRISM](https://prismjs.com) for code syntax highlighting. PRISM is a very well know syntax highlighter. You most likely have visited many sites that are using it. If you are building a React site and would like to use it, one good solution is [react-syntax-highlighter](https://www.npmjs.com/package/react-syntax-highlighter).

This blog is also made with [Gatsby](https://www.gatsbyjs.org/) which requires Gatsby specific plug-ins to make use of PRISM. All posts/articles are written in [Markdown](https://en.wikipedia.org/wiki/Markdown). You can read more about the setup at [gatsby-remark-prismjs](https://www.npmjs.com/package/gatsby-remark-prismjs).

The main challenge for me was getting a syntax color theme I like and and figuring out how to implement it. I'm not sure I am 100% satisfied with the color theme, it is mostly like VS Code's Monokai Dimmed



# Prism test

## CSS

```css
/* css - comment */
:root {
  --primary-color: aqua;
}
li:first-of-type + li {
  color: var(--primary-color);
}
h1 {
  font-size: 24;
}
pre[class*='language-'] {
  overflow: auto;
  padding: 1.3125rem;
}

pre[class*='language-']::-moz-selection {
  /* Firefox */
  background: hsl(207, 4%, 16%);
}

.token.attr-name { /* HTML: attributes */
  color: rgb(173, 219, 103);
  font-style: italic;
}

#main {
  color: black;
}
```

## HTML

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <link href="prism.css" rel="stylesheet" />
  <title>Document</title>
</head>
<body>
  <!-- html comment -->
  <h1>Hello</h1>
  <div class="fake">
    <img src="http://some-place.com" alt="do not know" />
  </div>
  </body>
</html>
```

## Straight JS

```js
var a = 1
let b = 2
const c = 3
const d = true
const name = 'me'
const usingBackticks = `My name is ${me}`
const someUrl = 'http://some-url.com'
const SOME_CONST = 'const'

function someFunction(parm1, param2) {
  return param1 + param2
}
```

## JSX - Component

```jsx

import React, { Component } from 'react';
import logo from './logo.svg';
import './App.css';
import Hello from '../Hello'
import { compose } from 'recompose'

function getName = (id) => {
  return 'name'
}


class App extends Component {

  onClick = (param) => {
    return 1
  }
  render() {
    // Test stuff
    var a = 1
    let b = 2
    const c = 3
    const d = true
    const name = 'me'
    const usingBackticks = `My name is ${me}`
    const someUrl = 'http://some-url.com'

    return (
      <div className="App">
        <img src='http://my.com' />
        <header className='App-header'>
         <Hello />
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
          <button onClick={this.onClick}>Say hello</button>
        </header>
      </div>
    );
  }
}

export default App;

```


