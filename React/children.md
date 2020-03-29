## Get React children

```javascript
class Grid extends React.Component {
  render() {
    return <div>{this.props.children}</div>
  }
}
```

### Manipulate 
Can use React.Children.map or React.Children.forEach

```javascript
class IgnoreFirstChild extends React.Component {
  render() {
    const children = this.props.children
    return (
      <div>
        {React.Children.map(children, (child, i) => {
          // ignore first children
          if (i < 1) return
          return child
        })}
      </div>
    )
  }
}
```
```jsx
<IgnoreFirstChild>
  <h1>First</h1>
  <h1>Second</h1> // <- Only this is rendered
</IgnoreFirstChild>
```

### Conver to array
```jsx
class Sort extends React.Component {
  render() {
    const children = React.Children.toArray(this.props.children)
    return <p>{children.sort().join(' ')}</p>
  }
}
<Sort>
  {'bananas'}{'oranges'}{'apples'}
</Sort>
