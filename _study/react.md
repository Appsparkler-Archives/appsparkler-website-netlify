---
layout: post
title: React
categories: study react
---
# Glossary
  - [React](#react-notes)
  - [React Dom Router](#react-dom-router)
  - [Redux](#redux)
  - [Context API](#context-api)
  - [React Hooks](#react-hooks)

## React Notes
- HOC or HIGHER ORDER COMPONENTS:
  - A higher-order component (HOC) is an advanced technique in React for reusing component logic. HOCs are not part of the React API, per se. They are a pattern that emerges from React’s compositional nature.
  - These are basically `functions` that take a `React Component` as an argument and return a `Modified React Component`
  - IMPLEMENTATION EXAMPLE (double-wrap):
    ```jsx
      // Containerify.react.js
      const containerify = (Component)=> (
        <div className="container">
          <Component />
        </div>
      )
      // Cardify.react.js
      // I wanted to wrap various components with div.card div.card-content
      const cardify = (Component)=> (
        <div className="card">
          <div className="card-content">
            <Component />
          </div>
        </div>
      )
      // Signup.react.js
      ...
      export default containerify(cardify(SignUp))
    ```
  - ANOTHER implementations wa
- REACT CLASS
  - CONSTRUCTOR 
    - It is recommended that `state` should ideally be set inside the `constructor` function
- STATE
  - INITIALIZING STATE:
    - STATE can be initialized with a class variable, like so:
    ```javascript
      this.state = {
        // all initial data data and expected `keys` go here.
      }
    ```
  - SETTING STATE:
    - STATE can be set with the `this.setState()` method.  This is usually done inside the class-constructor:
      ```javascript
        this.setState({
          // new state goes here 
        })
      ```
- PROPS
  - `props` is available on `class-components` by default:

    ```javascript
      // for ex. (inside a class component...)
      ...
      componentDidMount() {
        console.log(this.props) // yay! props is available by default    
      }
      ...
    ```
- COMPONENT LIFE CYCLE
  - `MOUNTING`
    - `componentDidMount()` - This method is called as soon as the component is mounted (inserted into the DOM-tree)
      - Initialization that requires DOM nodes goes here.
      - If we need to load data from a remote-end point, this is a good place to instantiate the network request.
  - `UPDATING`
  - `UNMOUNTING`

- REFS
  - How to set ref (a reference to an element in the component's dom)?
  - Reference Links: [David Walsh's blog](https://davidwalsh.name/get-react-component-element)
  - CREATE a `ref` (most probably in the constructor) - `this.carouselRef = React.createRef()`
  - SET this ref on any the element which we would like to have a reference to:
    ```jsx
      ...
      <div className="carousel" ref={this.carouselRef}>
        ...
      </div>
      ...
    ```
   - ACCESS the `element` with the created `ref`
    ```jsx
      ...
      const carousel = this.carouselRef.current // this will have the DOM element
      ...
    ```
## React-Dom-Router
- `<SWITCH>`
  - This feature solves the problem of loading more than one component for a `<Route>`.
  - Usage:
    ```jsx
      <Switch>
        <Route path="/contact" component={Contact}>
        <Route paht="/:post_id" component={Post}>
      </Switch>
    ```
  - Without `<Switch>` the path `/contact` would load two components - `Contact` and `Post` as the router would assume that `contact` is also a `post_id`.  With `<Switch>`, the router will resolve the the first route it gets starting from top and once resolved, it will not try to resolve any more routes.
- `PARAMS`
  - Router properties and methods on the params:
    - PROPERTIES - 
      - `MATCH` [Reference Link](https://reacttraining.com/react-router/web/api/match)
      - `HISTORY` - [Reference Link](https://reacttraining.com/react-router/web/api/history)
- MATCHING exact routes - Sometimes we may face the issue that the project less strict route is listed above the more strict one.  For ex. `path="/"` is listed before `path="/project/:id"` - this causes an issue that the `/dashboard` doesn't get rendered even though `<Switch>` is wrapped around it.  In this case we need to add an attribute `exact` to the `Route`, like so:
  ```jsx
    ...
    <Route exact path="/" component={Dashboard} /> {/*note the 'exact' attribute here */}
    <Route path="/project/:id" component={ProjectDetails} />
    ...
  ```

### How to?
- PASS `data/state` to `<Link ... >`:
  - [`Link to` Object](https://reacttraining.com/react-router/web/api/Link/to-object)
  - Example:
    ```jsx
      // passing the state/data
      ...
      <Link to={
        pathname: `/post/${id}`,
        state: {foo: 'bar'}
      } >
        //
      </Link>
      ...
      // accessing the state/date
      ...
      alert(props.location.state)
      ...
    ```
   
- SETUP a SPA
  - DEFINE the `Route`(s) for the `BrowserRouter` in the `App` Component
    - SET the route
    - SET the component that needs to be loaded for each route
    - SET any other info as per the API for `Route`
    - For ex.
      ```jsx
      import { BrowserRouter, Route } from 'react-dom-router'
      ...
      <BrowserRouter>
        <div className='App'>
          <Navbar />
          // ROUTES
          <Route exact path="/" component={Home} />
          <Route path="/contact" component={Contact}/>
          <Route path="/about" component={About} />
          <Route name='post' path="/post/:post_id" component={Post} /> // DYNAMIC LINK
        </div>
      </BrowserRouter>
      ...
      ```
  - ADD the links for to the `Routes` for various `Link`
    - For ex.
    ```jsx
      <!-- STATIC-LINK -->
      <Link to="/about">About</Link>
      <!-- DYNAMIC-LINK -->
      <Link to={`/post/${post_id}`}>Read Post</Link>
    ```
    
## Redux
- STORE
  - A Redux-store is made up of `store`, `actions` and `reducers`.
    - `store` - is the `data-repository`
    - `actions` - are the interfaces that provide data to `reducers` to update the `store`
    - `reducers` - are methods that mutate the store.
- How to setup the store?
  - CREATE the store with the `createStore` method in `redux`.  It is created by passing a `reducer-function` to the `createStore` method (What good is a store without a `reducer`??)
  - SET initial state of the store
    ```javascript
      import { createStore } from 'redux'
      const initialState = {
        // it is a good practice to put all keys we may want to work with in the future
        posts: [],
        todos: []
      }
      const store = createStore(storeReducer)
      export default store
      // store Reducer
      function storeReducer(state = initialState, action) {
        if(action.type === 'ADD_TODO') addTodoToState.call(null, state, action.todo)
        if(action.type === 'ADD_POST') addPostToState.call(null, state, action.post)
      }
      // 
      function addTodoToState(state, todo) {
        return {
          ...state,
          todo: [...state.todos, todo]
        }
      }
      function addPostToState(state, post) {
        return {
          ...state,
          post: [...state.posts, post]
        }
      }
      
    ```
- How to integrate the Redux store with React application?
  - [Reference Link](https://www.youtube.com/watch?v=f87wPQMgF4c&list=PL4cUxeGkcC9ij8CfkAY2RAGb-tmkNwQHG&index=39)
  - INSTALL the `react-redux` node module
  - WRAP the component that needs to be integrated with the store with the `<Provider>` component from `react-redux`
  - PASS the store to the wrapper `<Provider>` component:
    ```jsx
    ...
    import { createStore } from 'redux'
    import { Provider } from 'react-redux`
    import store from './store'
    ...

    ReactDOM.render(
      <Provider store={store}>
        <App>
      </Provider>
      , document.getElementById('root')
     )
    ```
- How to access the `store`'s `state/data` and/or `action` inside a React Component?
  - [Reference Link](https://www.youtube.com/watch?v=CZ2qGtAnhoE&list=PL4cUxeGkcC9ij8CfkAY2RAGb-tmkNwQHG&index=40)
  - CONNECT the `state` in the store with the `connect` higher-order-component from `react-redux`
  - CREATE a connector function that `maps-state-to-props` - This function returns only the `state` that we need for the component. 
  - CREATE a connector function that `maps-actions-to-props` - This function returns only the `action` (dispatchers) that we need for the component.
  - ACCESS the data on `props` from inside the component
  ```jsx
    ...
    import { connect } from 'react-redux'
    ...
    class MyComponent extends React.Component {
      render() {
        ...
        alert(this.props.posts); //this is the posts from the store's state/data
        ...
      }
    }
    const mapStateToProps = state => {
      return {
        posts: state.posts
      }
    }
    
    const mapDispatchToProps = (dispatch, ownProps) => {
      return {
        addPost: post => dispatch({type: 'ADD_POST', post})
      }
    }
    
    export default connect(mapStateToProps, mapActionToProps)(MyComponent) 
    ...
  ```
- How to access `component-props` in the `connector` method?
  - [Reference Link](https://www.youtube.com/watch?v=SoOTQW4-tYk&list=PL4cUxeGkcC9ij8CfkAY2RAGb-tmkNwQHG&index=41)
  - ACCESS the `components props` as  `connector` methods second argument:
    ```jsx
      ...
      const maptStateToProps = (state, ownProps) => {
        const id = ownProps.match.params.post_id
        return {
          post: state.posts.find(post => post.id === id)
        }
      }
      export default connect(mapStateToProps)(MyComponent)
    ```
 - How to setup the `root reducer`?
  - [Reference Links] - [Net Ninja Tutorial](https://www.youtube.com/watch?v=hOQ7x_X2gIg&list=PL4cUxeGkcC9iWstfXntcj8f-dFZ4UtlN3&index=11)
  - SETUP various reducers for different parts of the project.  For ex:
    - `/store/reducers/project.js`
    - `/store/reducers/auth.js`
  - COMBINE these reducers in a `root` reducer with the `combineReducers` of `redux`:
    - `/store/reducers/root.js`
      ```javascript
        import {combineReducers} from 'redux'
        import project from './project'
        import autho from './auth'
        
        export default combineReducers({
          project,
          auth
        })
      ```
      
### :whale: Deploying an App created with `create-react-app` on `Heroku`:
- CREATE an APP with `create-react-app` - `npx create-react-app my-app`
- CD into the APP: `cd my-app`
- CREATE a `heroku app` - `heroku apps:create my-app`
- CREATE a `heroku pipline` for our app - `heroku piplines:create my-pipline -a my-app`
- ADD the `heroku buildpack` for our app - `heroku buildpacks:set https://github.com/mars/create-react-app-buildpack.git -a my-app`
- CREATE the GitHub Repository on [GitHub](https://github.com)
- SET a remote address for the git repo - `git remote add origin <origin>`
- SET the pipeline on heroku for the app which will build from the master branch of newly create github repo
- PUSH the code to GITHUB - `git push origin head`
- You should see your react-app on your heroku app
- Examples - 
  1. [MarioPlan](https://appsparkler-marioplan.herokuapp.com)
  1. [PS Leaderboard](https://ps-leaderboard.herokuapp.com)


## Context API
- Context API is an OOTB feature provided by React which is an Redux type centeralized data-store.  It is recommended to store only global-type data in the context-data-store - data such as `theme, globals, authenticated-user, etc`
### Setting up the context:  
  - CREATE the `context` with `creatContext` method provided by `react`:  
  ```javascript
      import React, {createContext} from 'react'
      ...
      export const ThemeContext = createContext(); // notice that we are exporting the created-context
  ```  
    
  - CREATE the `context-provider-component` and set-up the `state` (with default values, if required) in it:  
  ```javascript
    ...
    export default class ThemeContextProvider extends Component {
      constructor(props){
        super(props);
        this.state = {
          theme: 'dark'
        }
      }

      render(){
        return(
          <ThemeContext.Provider value={{...this.state}}>
            {this.props.children}
          </ThemeContext.Provider>
        )
      }
    }
  ```
  - IMPORT the `ThemeContextProvider` component and wrap it around the components that are expected to utilize the `context`:
  ```javascript
  // App.js
  ...
  import ThemeContextProvider from '../context/ThemeContext.react'
  ...
  export default class App extends Component {
    ...
    render() {
      return(
        <div className="App">
          <ThemeContextProvider>
            <Navbar />
            <BookList />
          </ThemeContextProvider>
        </div>
      )
    }
  }
  ```
  - ACCESS the `context` in the components that are expected to consume the contextual data:
  ```javascript
    import {ThemeContext} from '../../context/ThemeContext.react'
    ...
    export default class BookList extends Component{
      static contextType = ThemeContext
      render() {
        const {theme} = this.context
        <div className={`list-group-${theme}`}>
          ...
        </div>
      }
    }
  ```
  
  ## An alternate approach to access the context:
  - With this approach we do not need to set `static contextType = <Context>`.  Instead we work with the `Consumer` property of the `Context`.  For ex:  
  ``` javascript
  ...
  import {ThemeContext} from '../context/ThemeContext.react'
  ...
    render() {
      return(
        <ThemeContext.Consumer>
          {
            (context) => (
              <div>JSON.stringify(context)</div>
            )
          }
        </ThemeContext.Consumer>
      )
    }
  ...
  ```

### React Hooks
1. Setting a `ContextProvider` : [POC Commits](https://github.com/appsparkler/poc/commit/348385f5ba350f59503cbfd06d427161a2e32603)
1. Accessing context with `static contextType` : [POC Commits](https://github.com/appsparkler/poc/commit/beac1a14f6de7a06bc633d9026bd19cf6fc66724)
1. Utilizing `contextType` in the app : [POC Commits](https://github.com/appsparkler/poc/commit/26dcdafc93ccb703fc7a78a2ab75932b4b9ab1e3)
1. Accessing context with `Consumer` : [POC Commits](https://github.com/appsparkler/poc/commit/8b41576c3cad6aafd8743200993b8f38dc2124ad)
1. Utilizing the Context - `Consumer`: [POC Commits](https://github.com/appsparkler/poc/commit/d5869654893ecc37bf90347d7a49aeaeb2babf41)
1. `useState` hook implementation : [POC Commits](https://github.com/appsparkler/poc/commit/8203954ffcba2397175f66338878393de363673d)
1. `useEffect` hook implementation : [POC Commits](https://github.com/appsparkler/poc/commit/dd92d707bf255e5ec6f8cb5a1d3fdc9c72ff06e0)
1. `useContext` hook implementation : [POC Commits](https://github.com/appsparkler/poc/commit/3e8273c3bd7c8a8c6c4df21bd16ca1d4e617cdb0)
1. Multiple Contexts : [POC Commits](https://github.com/appsparkler/poc/commit/06ba8993b3f67f5e0ed5a39bae1d1dd433259a69)
1. Class component to Functional Component with Hooks : [POC Commits](https://github.com/appsparkler/poc/commit/70188b00d65d5cd9584a2941442cba63bee717d7)
1. Context-Component with functional components (instead of Class components): [POC Commits](https://github.com/appsparkler/poc/commit/e4ea9ad2560d4fbfd8fc79153aa68142a607572b)
1. Utilizing context created with functional components : [POC Commits](https://github.com/appsparkler/poc/commit/9c06d2695b84e1d3eed27110190fa853ff2f4ded)
1. Setting context  : [POC Commits](https://github.com/appsparkler/poc/commit/626fb935828e338440ccc053fc84a2af3ac2e746)
1. One Context, multiple components : [POC Commits](https://github.com/appsparkler/poc/commit/69e17d305d13af5e6b99b567de87e80bec314748)
1. Context from scratch : [POC Commits](https://github.com/appsparkler/poc/commit/d301e958ca49b3289af7d8832c6be3708d30f833)
1. Components that will utilize context : [POC Commits](https://github.com/appsparkler/poc/commit/105a63eb741b74d68dc37eb29d35427cb82beda6)
1. Context + Components for Movies : [POC Commits](https://github.com/appsparkler/poc/commit/626fb935828e338440ccc053fc84a2af3ac2e746)
1. A different approact to work with components: [POC Commits](https://github.com/appsparkler/poc/commit/a759f98b82dd2b4b65d633587723978fd82566ef)
1. `useReducer` React hook - [POC Commits](https://github.com/appsparkler/poc/commit/ddbec0a2aa772b69ae5ea15627768dfb6f155639)
1. Root-Context - [POC Commits](https://github.com/appsparkler/poc/commit/7c68fc3a313005625a276e2273b6e2f62f53b0f1)
1. Custom Hook (`useSelector`) - [POC Commits](https://github.com/appsparkler/poc/commit/9cbee26904ce336eb2e0f0bf5c16904fddf06695)

