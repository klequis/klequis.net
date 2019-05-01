---
title: 5. React with TypeScript & Redux Part 1
date: '2019-04-03'
spoiler: Don't know yet
---

#4

**Diving in!**

> After each change I'm restarting the app to make sure it boots

# Create default project using Create React App

Straight from the [Create React App doc](https://facebook.github.io/create-react-app/docs/adding-typescript).

```js
npx create-react-app cra1 --typescript

cd cra1

npm install --save typescript @types/node @types/react @types/react-dom @types/jest

cd src

mv index.js index.tsx

mv App.js App.tsx

cd ..

npm start
```

I also like to swap out Yarn for npm. Not sure deleting /node_modules is necessary but can't hurt.

```js
rm -rf node_modules

rm yarn.lock

npm i

npm start
```

# Eject it

```js
npm run eject
```

# `tsconfig.json` in alphabetical order
Since I'm comparing `tsconfig.json` to other project in order to create the final configuration I like to have it in alphabetical order. Here it is:

```json
{
  "compilerOptions": {
    "allowJs": true,
    "allowSyntheticDefaultImports": true,
    "esModuleInterop": true,
    "forceConsistentCasingInFileNames": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "lib": [
      "dom",
      "dom.iterable",
      "esnext"
    ],
    "module": "esnext",
    "moduleResolution": "node",
    "noEmit": true,
    "resolveJsonModule": true,
    "skipLibCheck": true,
    "strict": true,
    "target": "es5"
  },
  "include": [
    "src"
  ]
}
```

# Enable and use absolute imports

Add to `tsconfig.js`
```json
"baseUrl": "./src",
```

Modify `package.json`
```json
"start": "export NODE_PATH=src && node scripts/start.js",
"build": "export NODE_PATH=src && node scripts/build.js",
"test": "export NODE_PATH=src && node scripts/test.js --env=jsdom"
```

# Add `react-jss`

```js
npm i -S react-jss@10.0.0-alpha.16
```

> `react-jss ` has it types built-in. Do not add `@types/react-jss` as they are not compatible with `react-jss` version 10.

## Give it a try

Change Hello.tsx to be like this
```js
import * as React from 'react'
import withStyles, {WithStyles} from 'react-jss'

const styles = {
  h1Color: {
    color: 'green'
  }
}

interface IProps extends WithStyles<typeof styles> {

}

const Hello: React.FunctionComponent<IProps> = ({ classes }) => {
  return <h1 className={classes.h1Color}>HI</h1>
}

export default withStyles(styles)(Hello)
```





