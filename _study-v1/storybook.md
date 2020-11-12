---
layout: post
title: Storybook
categories: study storybook
---

## The `export default` in `stories`:
  1. component -- the component itself,
  1. title -- how to refer to the component in the sidebar of the Storybook app,
  1. excludeStories -- exports in the story file that should not be rendered as stories by Storybook.
  1. argTypes -- specify the args behavior in each story.

## The `preview.js` file:
parameters are typically used to control the behavior of Storybook's features and addons. In our case we're going to use them to configure how the actions (mocked callbacks) are handled.
For ex:
```javascript
export const parameters = {
  actions: { argTypesRegex: '^on[A-Z].*' },
};
```
This will pro-actively configure the `action` for all handlers that start with `on`  - for ex. `onClick`, `onTimezoneUpdated`, `onOpen,` etc.

## Developing Workflow
1. Build `components`
1. Build `stories` from `components`
1. Setup `templates` for `stories`
1. Export all `variants` for the component with `templates`
1. Import the `variants` in `stories` of parent-components to setup `parent-component-variants`.
1. Ensure snapshots for all stories with `@storybook/addons-storyshots`
1. Ensure `actions` are pre-configured so that we don't have to include events for components.
1. Write automated tests for rendering scenarios.
1. 


## `args`
I think of `args` as building blocks for stories - they form the `data-chain` from the root of the application until its extreme periphery.
