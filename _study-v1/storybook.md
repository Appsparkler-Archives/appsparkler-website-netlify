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
