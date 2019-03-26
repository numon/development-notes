##Component lifecycle 

getDerivedStateFromProps(props, state) sync state
shouldComponentUpdate(nextProps, nextState) may cancel updating process
getSnapshotBeforeUpdate(prevProps, prevState) last-minute DOM ops
render()
Update Child Component Props
componentWillUnmount()
componentDidUpdate() CAse side-effects
componentDidMount()
