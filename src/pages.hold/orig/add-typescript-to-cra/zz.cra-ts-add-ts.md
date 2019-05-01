Combining Microsft TypeScript React Starter with Create React App


**starting with cra-typescript**

- Make a copy of cra-typescript and name it the folder cra-ts-add-ts


```js
$ rm yarn.locl
$ rm -rf node_modules
$ npm i
```

Rmove from package.json

```json
"eslint": "5.12.0",
"eslint-config-react-app": "^3.0.8",
"eslint-loader": "2.1.1",
"eslint-plugin-flowtype": "2.50.1",
"eslint-plugin-import": "2.14.0",
"eslint-plugin-jsx-a11y": "6.1.2",
"eslint-plugin-react": "7.12.4",
```

Add TypeScript related files

```js

$ npm i -S @types/jest @types/node @types/react @types/react-dom ts-jest ts-loader tslint tslint-config-prettier tslint-react typescript

```