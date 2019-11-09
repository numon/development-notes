

## Route


Simple code:

```jsx harmony
    <BrowserRouter basename='/'>
      <News/>
    </BrowserRouter>
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
    
```

```jsx harmony
    <NavLink to='/' activeClassName='new-active'>Home</Link>
    
```

HOC to get all props from Router component
```jsx harmony
    withRouter(news); 
```

`<Switch />` - Load only one Route component 


```jsx harmony
    this.protps.history.push(pathname: '/'+ id);
```

