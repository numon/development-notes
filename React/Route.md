

## Route


Simple code:

```jsx harmony
    <BrowserRouter basename='/'>
      <News/>
    </BrowserRouter>
```

```jsx harmony
    <Switch /> - only one Route load 
```


```jsx harmony
    this.props.history.push() - works as active link 
```

```jsx harmony
    <Route path="/" exact render={()=><h1>Home</h1>} />
    <Route path="/" exact component={Posts} />
    <Route path="/:id" component={post} />
    <Route path = {this.protps.math.url + '/:id'} />
```

```jsx harmony
    <Link to="/">Home</Link>
    <Link to={
      pathname: '/news',
      hash: '#Load More',
      search: '?quick-search=true'
    }>Home</Link>
    
    this.props.match.url + '/new-post'
    
```

```jsx harmony
    //for styling 
    <NavLink to='/' activeClassName='new-active'>Home</Link>
    
```

HOC to get all props from Router component
```jsx harmony
    // add props with Route - history
    withRouter(news); 
```

`<Switch />` - Load only one Route component 


```jsx harmony
    this.protps.history.push(pathname: '/'+ id);
```

