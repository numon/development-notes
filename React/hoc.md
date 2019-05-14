# HOC

## Simple example of HOC

```javascript
export const hoc(Component, props) => {
  return () => {
    return <Component {...props} enchanted={true} />
  }
} 
```

## Lazy loading component

```jsx harmony
const asyncComponent = (importComponent) => {
  return class extendes Component {
    state = {
      component: null;
    }
    
    componentDidMount() {
      importComponent().then(cmp => this.setState({ component: cmp.default }))
    }
    
    render () {
      const C = this.state.component;
      return C ? <C {...this.props} /> : null;
    }
  }
}

//use 

const NewPost = asyncComponent(() => {
  return import('./Path/to/Component');
});

<Route path='news' component={NewPost} />

```

## Lazy loading with React v16

```jsx harmony
const Posts = React.lazy(() => import('./components/Posts'));

<Route path='/posts' render={() => (
  <Suspense fallback={<div>Loading...</div>}>
    <Posts />
  </Suspense>
  )}
  />
```
