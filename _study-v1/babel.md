---
layout: post
title: Babel
categories: study babel
---

### `.babelrc.js` file
  - Reference Links - [Babel-Preset-Env](https://babeljs.io/docs/en/babel-preset-env)
  - Defining presets:
    ```javascript
    // .babelrc.js
    module.exports = {
      presets: ['preset-env', 'preset-react']
    }
    OR
    module.exports = {
      presets: [['preset-env', {
        // configuration for preset-env
        targets: {
          node: 'current'
        }
      }], 'preset-react']
    }
    ```

# Issue Resolution
- If you face an issue with `regeneratorRuntime is not defined/undefined`; install the `@babel/plugin-transform-runtime` plugin and then add the following options in `.babelrc.js`
```javascript
//...
['@babel/plugin-transform-runtime`, {regenerator: true}]
//...
```
