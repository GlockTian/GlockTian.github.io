---
layout: post
title: "Code Format"
subtitle: "Enable Auto Code Format in NodeJS project"
date: 2022-07-01 21:45:13 -0400
background: '/img/posts/06.jpg'
tags: [NodeJs]
---

# What are they?
- **ESLint is** a tool for identifying and reporting on patterns found in ECMAScript/JavaScript code, with the goal of making code more consistent and avoiding bugs.
- **Prettier** is an opinionated code formatter
- **Husky** supports all Git hooks. You can use it to lint your commit messages, run tests, lint code, etc... when you commit or push.

├── src

├── public

├── .husky

│   ├── views

│       ├── pre-commit

├── .prettierrc.js

├── package.json

├── package-lock.json 

└── .gitignore

## in `package.json` we need

```json
"devDependencies": {
  "husky": "^7.0.0",
  "lint-staged": "^12.3.7",
  "npm-run-all": "^4.1.5",
  "prettier": "2.6.0"
},
"lint-staged": {
  "*.{js,css,md,jsx}": "prettier --write"
},
```

## in `.husky/pre-commit` we need
```sh
#!/bin/sh
. "$(dirname "$0")/_/husky.sh"

npx lint-staged
```

## in `.prettierrc.js` we need

```js
module.exports = {
  trailingComma: "es5",
  tabWidth: 2,
  semi: true,
  singleQuote: false,
  useTabs: false,
};
```