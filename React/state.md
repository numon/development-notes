

```jsx harmony
const inputHandler = (event, inputID) => {
  const updatedForm = {...this.state.form};
  const updatedElement = {...updatedForm[inputID]};
  updatedElement.value = event.target.value;
  updatedForm[inputID] = updatedElement;
  this.setState({form: updatedForm});
}
```
