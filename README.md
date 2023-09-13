## classes vs hooks
> with hooks you don't have to worry about "this" anymore.

> no more method bindings
```js
export class ShowCount extends React.Component {
    constructor(props) {
        super(props)
        this.state = {
            count: 0
        }
        this.handleClickEvent = this.handleClickEvent.bind(this);
    }
    componentDidMount() {
        this.setState({
            count: this.props.count
        })
    }
    handleClickEvent = () => {
      this.setState({count: this.state.count + 1});
    }
    render() {
        return (<button onClick={this.handleClickEvent}>Count: {this.state.count}</button>)
    }
}
```
> hooks have less boilerplate

> extract logic of component

> you can simplefy  

|Functions|Clases|
|---|---|
|no more method bindings| -- |
|returns jsx in the return statemant|requires a reder() function|
|do not have lifecycle functions|have lifecycle functions|
|requires useState() hook for state|allows state management|

## Lifecycle Methods
### Mounting
When an instace of a componet is being created and inserted into the DOM, MountingFace have 4 methods:
- constructor
    - A special function that will get called whenever a new component is created.
    - Initializing state
    - bindings the event handlers
    - Do not cause side effects. Ex: HTTP requests
```js
constructor(props) {
    super(props)
    this.state = {
        count: 0
    }
    this.handleClickEvent = this.handleClickEvent.bind(this);
}
```
- static getDerivedStateFromProps
    - When the state of component depends on changes in props over time.
```js
static getDerivedStateFromProps(props, state) {
    if (props.name !== state.name) {
        return { // return new state
            name: props.name
        }
    } 
    return null
}
```
- render
    - only required method in clasese
    - read props & state and return jsx
```js
render() {
    return (<button onClick={this.handleClickEvent}>Count: {this.state.count}</button>)
}
```
- componentDidMount
    - called only ones in the lifecycle methods
    - Invoked immediately after a component and all its chlidren components have been rendered to the DOM
    - causes side effects === HTTP requests


### Updating
When a component is being re-rendered as a result of changes to either its props or state, UpdatingFace 5 methods
- static getDerivedStateFromProps
    - Method is called every time a component in re-rendered 
- shouldComponetUpdate
    - dictates if the component should re-render or not 
    - performance optimizations
```js
shouldComponetUpdate(nextProps, nextState) {
    return false // false or true
}
```
- render
- getSnaphotBeforeUpdate
    - called right before the changes from the virtual DOM are to be reflected in the DOM
    - capture some information from the DOM
    - method will eithre return null or return a value. Returned value will be pased as the third parameter to the next method
```js
getSnaphotBeforeUpdate(prevProps, prevStata) {
    return null // null or value to componentDidUpdate, third parameter snapshot
}
```
- componentDidUpdate
    - called after the render is fininshed in the re-render cycles
```js
componentDidUpdate(prevProps, prevState, snapshot) { console.log(ee) }
```

### Unmounting
When a component is being romeved from DOM UnmountingFace: 
- componentWillUnmount
    - Method is invoked immediately bofero a component is unmounted and  destroyed
    - cancelling any network request, removing event handlers, cancelling any subscription and also invalidating timers
<br />

### Error Handling
When there is an error during redering, in a lifecycle method, or in the constructor of any child componentDidUpdate
- static getDerivedStateFromError 
    - When there is an error either durnig rendering, in a lifecycle monthod, or in the constructor of any child component
- componentDidCatch
    - When there is an error either durnig rendering, in a lifecycle monthod, or in the constructor of any child component

