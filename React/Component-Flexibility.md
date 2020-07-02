## AS example simple list component with multiple re-suing of it 

```jsx harmony

import React from 'react';

function ListRoot({children, ...rest}) {
  return <div {...rest}>{children}</div>
}

function ListHeader({children}) {
  return <h5>{children}</h5>
}

function ListItem({children, ...rest}) {
  return <li {...rest}>{children}</li>
}

function ListComponent({label, items = [], collapsed, toggle, limit, total, renderListItem}) {

  return (
    <ul>
      <p>{label}</p>
      {items.map((member) =>
        renderListItem
          ? <React.Fragment key={member}>{renderListItem(member)}</React.Fragment>
          : <ListItem key={member}>{member}</ListItem>
      )}
      {total > limit && (
        <ListItem className="expand">
          <button type="button" onClick={toggle}>
            {collapsed ? 'Expand' : 'Collapse'}
          </button>
        </ListItem>
      )}
    </ul>
  )
}

export default function List(
  {
    component: RootComponent = ListRoot,
    collapsed,
    toggle,
    header,
    label,
    items = [],
    limit = 3,
    RenderHeader,
    RenderList,
    renderListItem
  }) {

  return (
    <RootComponent>
      {RenderHeader
        ? RenderHeader()
        : <ListHeader>{header}</ListHeader>
      }
      {
        RenderList
          ? RenderList()
          : <ListComponent
            label={label}
            items={
              collapsed && items.length > limit ? items.slice(0, limit) : items
            }
            collapsed={collapsed}
            toggle={toggle}
            limit={limit}
            total={items.length}
            renderListItem={renderListItem}
          />
      }

    </RootComponent>
  )
}
```

using current component
```jsx
    <div className="root">
      <div className="listContainer">
        <List
          component={BeautifulListContainer}
          collapsed={collapsed}
          toggle={toggle}
          header={null}
          label="Bidders"
          items={pediatricians}
          limit={limit}
        />
      </div>
      <div className="listContainer">
        <List header="Bids on" label="Bidders" items={psychiatrists} />
      </div>
    </div>
```
