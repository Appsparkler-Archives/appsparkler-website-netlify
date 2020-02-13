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


### Javascript Notes
## Pass `params` in curly braces and work with `structuring` and `destructuring`

```javascript
doThis({expiryDate, effectiveDate}) // Better structure (can be accessed in any order

doThis(expiryDate, effectiveDate) // Will have to be accessed from the available order
```

## Work with `&&` and `||` to set values:
```javascript
 const effectiveTime = instance && instance.effectiveTime; // will set the last available value if the previous values are available (for ex. will set instance.effectiveTime if instance is available.
 const expiryTime = selectedInstance.expiryTime || instance.expiryTime // will set the first available value.  For ex. will set the selecedInstance.expiryTime if it is available.  ONLY if it is not available it will set the instance.expirtyTime
```

## Destructure within the `curly-braces`
```javascript
function doSomething(state) {
  const {data, username, email} = state;
  doSomethingElse(state) // state object is readily availble
}

function doSomething({data, username, email}) {
  // this looks shorter initially; however, now you dont have access to the component `state` object
}
```

## Pass as few arguments as possible
```javascript
// better approach
function myHook() {
  const [month, setMonth] = React.useState()
  const [setDay, setDay] = Reactt.useState()
  const [setEvent, setEvent] = React.useState()
  const states = {
    month, setMonth,
    setDay, setDay,
    setEvent, setEvent
  }
  setEventOnDay(states); // the setEventOnDay can utilize what it needs
  setMonthWithDay(states); // the setMonthWithDay can utilize what it needs
}

// previous approach
function myHook() {
  const [month, setMonth] = React.useState()
  const [setDay, setDay] = Reactt.useState()
  const [setEvent, setEvent] = React.useState()
  setEventOnDay({setEvent, event, day, setDay})
  setMonthWithDay({setDay, day, setMonth});
}
```



## CSS
## SVG `height`, `width` and `fill`:
The ideal way to give correct dimensions to `SVG` is with wrapping it.  For ex:
```sass
span.svg-wrapper
  height: 16px
  width: 16px
  svg
    height: 100%
    width: 100%
    path
      fill: blue
```
