<div align="center">
<h1>jest intro</h1>

<a href="https://www.emojione.com/emoji/1f989">
  <img
    height="80"
    width="80"
    alt="owl"
    src="https://raw.githubusercontent.com/testing-library/jest-dom/master/other/owl.png"
  />
</a>

<p>Custom config files, setup, tips and tricks to start a testable project with Jest</p>

</div>

---

## Table of Contents
- [Introduction](#introduction)
- [The Philosophy](#the-philosophy)
- [Scripts](#scripts)
  - [`Istanbul`](#istanbul)
- [Babel](#babel)
  - [`Setup`](#setup)
    - [`Tip`](#tip)
  - [`Advanced Settings`](#advanced-settings)
  - [`Different libraries syntax`](#different-librairies-syntax)
 







## Introduction 

Jest is a delightful JavaScript Testing Framework with a focus on simplicity. It works with projects using: Babel, TypeScript, Node, React, Angular, Vue and more!

By ensuring your tests have unique global state, Jest can reliably run tests in parallel. To make things quick, Jest runs previously failed tests first and re-organizes runs based on how long test files take.

Generate code coverage by adding the flag --coverage. No additional setup needed. Jest can collect code coverage information from entire projects, including untested files.

Jest uses a custom resolver for imports in your tests, making it simple to mock any object outside of your test’s scope. You can use mocked imports with the rich Mock Functions API to spy on function calls with readable test syntax.

## The Philosophy 

Jest is a JavaScript testing framework designed to ensure correctness of any JavaScript codebase. It allows you to write tests with an approachable, familiar and feature-rich API that gives you results quickly.

Jest is well-documented, requires little configuration and can be extended to match your requirements.

Jest makes testing delightful.







> Jest is a pretty big package, Pure javascript. There's no DOM API for example, that's why we need to include jsdom env in it. 


<hr />

## scripts:

` "test": "jest"`
` "test:watch": "jest --watch" `

` "test:coverage": "jest --coverage" ` to access to istanbul, ` coverage/lcov-report/index.html `

`"test": "react-scripts test --env=jsdom"` with Create React App

<hr />

#### istanbul 
To  access of the Istanbul report, hit the command: 
  ` start coverage/lcov-report/index.html ` 
If it shows a display issue on the browser, we have the possibility to hit : 
  ` CI=true npm run test ` or ` CI=true npm run test --coverage `

> Istanbul shows a "recap" of our tests with a graphic interface, displayed on the browser.


<hr />

## Babel

### Setup

> touch ` .babelrc` on root directory
> install: ` yarn --dev babel-core babel-preset-env ` with npm ` npm install --save-dev ... ` 

> loader: ` babel-loader `
> react: ` babel-preset-react `

#### Tip to use pure javascript syntax on .babelrc configuration

set .babelrc to a .js file, set on ` package.json ` :

```json
"babel": { "presets": "./.babelrc.js },
```

### Advanced settings for .babelrc.js:

> configuration on .babelrc.js: 
```javascript 
/* presets .babelrc.js on package.json */
const isTest = String(process.env.NODE_ENV) === 'test';
    
    module.exports = {
      /* Env plugin modules config
         Tree shaking */
      presets: [['env', { modules: isTest ? 'commonjs' : false }], 'react'],
      plugins: [
        'syntax-dynamic-import',
        'transform-class-properties',
        'transform-object-rest-spread',
        /* Dynamic imports config
        in plugins */
        isTest ? 'dynamic-import-node' : null
      ].filter(Boolean)
    };
```

> packages on package.json: 
```json
 "babel-plugin-dynamic-import-node": "1.2.0",
  "babel-plugin-syntax-dynamic-import": "6.18.0",
  "babel-plugin-transform-class-properties": "6.24.1",
  "babel-plugin-transform-object-rest-spread": "6.26.0",
```



### Different libraries syntax

* Jest : `test.only()` or `test.skip()`
* Mocka : `it.only()`  or `it.skip()`
* Jasmine : `iit()` or `xit()`