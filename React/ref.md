


Function in component 
```jsx harmony

    constructor() {
  this.inputElement = React.createRef( )
    }
    
    // in component 
    <Component ref={inputEL => {this.inputElement = inputEL}} />
    <Component ref={this.inputElement} />
```
