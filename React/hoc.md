

HOC

Please do not change default props of component:

```javascript
export const hoc(Component, props) => {
  return () => {
    return <Component {...props} enchanted={true} />
  }
} 
```

```javascript
function hoc(Component) {
  Component.defaultProps = 'someting';
  return enchanted(Component)
}
```

