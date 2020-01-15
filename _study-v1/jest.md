---
layout: post
title: Jest
categories: study jest
---

## Setting up Jest
- Reference Links - [Babel Setup](https://jestjs.io/docs/en/getting-started#using-babel)
- ENSURE a `.babelrc.js` config file is available as we will be testing `JSX` which are new `eslint-features`
  ```javascript
  module.exports = {
    presets: ['@babel/preset-env', '@babel/preset-react'] // for testing code written in ES6+ and with JSX 
  }
  ```
- INSTALL the required `@babel` packages - `@babel/preset-env`, `@babel/preset-react`

## Snapshot Testing Higher Order Components
  - IMPORT the `hoc` in the `test-file`.
  - CREATE a test-component and wrap it with the `hoc`:
    ```jsx
    it('should cardify the wrapped component correctly',() => {
      class TestComponent extends React.Component {
        render() {
          return (
            <div>A Test Component To Load</div>
          )
        }
      }
      const component = renderer.create(cardify(<TestComponent />))
      const tree = component.toJSON()
      expect(tree).toMatchSnapshot()
    })
    ```
    
## Snapshot Testing Components wrapped with Higher Order Components:
  - EXPORT two components from the wrapped component:
    1. The Base component 0 - `export const Signup = SignUp` 
    2. The wrapped component - `export const CardifiedSignup = cardify(SignUp)` 
  - TEST the `Base Component` at its location
  - TEST the `HOC Component` at its own location.

## How to test Components that are connected to `store` - both the main-component and its parent:
  - Reference Links - [`connect`ed-Component](https://github.com/appsparkler/poc/commit/047166191a136920acb96939429c3e45e6510d94#diff-1689acf8e01b897792dfdbdb379def70), [Parent of `connect`ed component](https://github.com/appsparkler/poc/commit/78d4be1b60e60768b29b3d8dc5e452ee21e831e9), [Corina's Blog](https://jsramblings.com/2018/01/15/3-ways-to-test-mapStateToProps-and-mapDispatchToProps.html)

## Matchers
  Matchers let us test values in different ways - for ex. `.toBe(...)` or `.not.toBe(...)`, `.equals(...)` or `.not.equals(...), etc.`
  - Reference Links - [Matchers](https://jestjs.io/docs/en/using-matchers), [Full List Of Matchers](https://jestjs.io/docs/en/expect), 
  - [Truthiness](https://jestjs.io/docs/en/using-matchers#truthiness) - sometimes need to distinguish between undefined, null, and false, but you sometimes do not want to treat these differently
  - [Numbers](https://jestjs.io/docs/en/using-matchers#numbers)
  - [Strings](https://jestjs.io/docs/en/using-matchers#strings)
  - [Arrays & Iterables](https://jestjs.io/docs/en/using-matchers#arrays-and-iterablesc)

## `jest` CLI (available by installing `npm i -g jest`
- INITIALIZING `jest` in a project - `jest --init`

## Snapshot Testing
- USE-CASE: _To test whether the output is correct_
- PREREQUISITES:
  - ENSURE Jest is [correctly setup](#setting-up-jest).
  - INSTALL `react-test-renderer` for generating snapshots.
- REFERENCE LINKS: [Snapshot-Testing](https://jestjs.io/docs/en/snapshot-testing), [Snapshot-Example](https://github.com/facebook/jest/tree/master/examples/snapshot), [Interactive Snapshot Mode](https://jestjs.io/docs/en/snapshot-testing#interactive-snapshot-mode), [Inline Snapshots](https://jestjs.io/docs/en/snapshot-testing#inline-snapshots), [Property Matchers](https://jestjs.io/docs/en/snapshot-testing#property-matchers), [Best Practices](https://jestjs.io/docs/en/snapshot-testing#best-practices), [Examples...](https://github.com/facebook/jest/blob/master/e2e/__tests__/console.test.ts)
- ABOUT: A typical snapshot test case for a mobile app renders a UI component, takes a snapshot, then compares it to a reference snapshot file stored alongside the test. The test will fail if the two snapshots do not match: either the change is unexpected, or the reference snapshot needs to be updated to the new version of the UI component.
- UPDATING SNAPSHOTS:
  - Reference Links : [Updating Snapshots](https://jestjs.io/docs/en/snapshot-testing#updating-snapshots)
  - ABOUT: A snapshot-test will fail if a bug has been introduced.  They can also fail when there is an implementation-change.  In that case wee need to update the snapshot.
  - EXECUTE `jest` with the following `--updateSnapshot` or `-u` flags to update the snapshots.
    - If we want to update only some snapshots, we can execute with `--testNamePattern` and pass the `test-name pattern` for which snapshots need to be updated.
- INLINE SNAPSHOTS:
  - ABOUT: Inline snapshots behave identically to external snapshots (.snap files), except the snapshot values are written automatically back into the source code. This means you can get the benefits of automatically generated snapshots without having to switch to an external file to make sure the correct value was written.
  - PREREQUISITE - `prettier` node_module is required.  `yarn add -D prettier`
  
## Testing Asynchronous code & Mocking
- Reference Links: [Tutorial](https://jestjs.io/docs/en/tutorial-async), [Working with `resolves`](https://jestjs.io/docs/en/tutorial-async#resolves), [Working with `async-await`](https://jestjs.io/docs/en/tutorial-async#async-await)

## Enzyme
- About: Enzyme is a JavaScript Testing utility for React that makes it easier to test your React Components' output. You can also manipulate, traverse, and in some ways simulate runtime given the output.
Enzyme's API is meant to be intuitive and flexible by mimicking jQuery's API for DOM manipulation and traversal. 
- Links: [Getting Started(React 16x)](https://airbnb.io/enzyme/docs/installation/react-16.html), [Enzyme implemented in MarioPlan](https://github.com/appsparkler/poc/commit/528e8d46d848fa6216bf302de439cd68adfb0e3f)
- Pre-Requisites:
  - INSTALL `enzyme` and `enzyme-adapter-react-16` (when working with React 16x)
  - CONFIGURE the plugin
    ```javascript
    ...
    import {configure} from 'enzyme'
    import Adapter from 'enzyme-adapter-react-16'
    
    configure({adapter: new Adapter()})
    ```
  - VISIT [Enzyme implemented in MarioPlan](https://github.com/appsparkler/poc/commit/528e8d46d848fa6216bf302de439cd68adfb0e3f) for an example implementation :smile:

## How To test a component that has a `<Link>` tag without a wrapping `<BrowserRouter>`?
* In the test, include the `BrowserRouter` in `imports`:
  ```jsx
  // Navbar.react.test.js
  import React from 'react`
  import { BrowserRouter as Router } from 'react-dom-router'
  import Navbar from '../Navbar.react'
  
  it('should render correctly', () => {
    expect.assertions(1)
    const component = renderer.create(
      <Router>
        <Navbar />
      </Router>
    )
    const tree = component.toJSON()
    expect(tree).toMatchInlineSnapshot()
  })
  ```
