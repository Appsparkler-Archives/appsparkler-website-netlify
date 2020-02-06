---
layout: post
title: Architecture
categories: study architecture
---

### :star: Pre-requisites
1. DEFINE the purpose
1. CREATE the design

### :whale: Project Setup
1. INITIALIZE `package.json` - `yarn init -y`
1. SETUP `.eslintrc.js`
1. SETUP `.babelrc.js`
1. SETUP `environment-variables`
1. SETUP and `auto-documentation` process
1. SETUP `CI-CD` pipeline
1. STRATEGIZE `error-handling`


## Notes
### Time
Handling time as per the time-zone is one of the essential aspects of project management.
- Convert the time to UTC when passing values to the database (think of it as centralized store; thus UTC)
  ```javascript  
    moment.utc(expiryDate).startOf('day').valueOf()
    // this will convert the expiryDate to UTC BoD
  ```
- Offset the UTC difference when rendering on users system (as it is local time)
  ```javascript
    moment(expiryDate).subtract(moment().offsetUTC(), 'minutes').valueOf()
    // here expiryDate is coming from the server (which will be as per UTC); thus we offset it to get the local time.
  ```
### CSS-hover-after
 ```sass
div
  :after
     background-color: green
     opacity: 1
  :after:hover
     opacity: .7
   
```
