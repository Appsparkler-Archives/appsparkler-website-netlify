---
layout: post
title: Atom IDE
categories: study ide atom
---

<style>
  code {
    border: 1px black solid;
  }
</style>
### How to replace dynamically with RegExp?
- [Reference Link](https://stackoverflow.com/questions/22220444/search-and-replace-with-regex-components-in-atom-editor)
- SEARCH with `RegExp` in `Atom IDE`. 
- WRAP the `dynamic-component` with `brackets`.  For ex. `:(.*):` - we want to replace `.*` component here. 
- REPLACE it by updating the replace-field: `$1|:$1:` this will replace, for ex. `:smile:` with `smile|:smile:` :smile: 
