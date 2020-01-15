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
