---
id: search-and-filter
title: Searching and Filtering
---

## Adding Search and Filter capabilities to your plugin
Many plugins need the ability to make their content search and filterable. Flipper provides a component for this use-case called `Searchable`. This is a higher-order-component that can be used to wrap any table, list, generic react-component and adds Flippers search bar on top of it.

We differentiate between search and filter, but both functionalities are provided by the `Searchable` component. Search is a custom string entered by the user. Filters can not be added by the user directly, but are added programmatically from within your plugin.

### Filters
Every filter has a key and a value. The key represents an attribute of the items you are filtering, and the value is the value that is compared with the items to see if the attribute matches. As an example, if you were filtering rows of a table, the a filter key would be the id of a column.

There are two different types of filters:

**include/exclude filters**: An arbitrary string that must (or must not) be included in the filterable item.

**enum**: Allows the user to select one or more from a set of values, using a dropdown.

### Higher Order Component
The `Searchable()` function adds three props to a React component:

`addFilter: (filter: Filter) => void`

Function allowing the component to add filters.

`searchTerm: string`

The search term entered into the searchbar by the user.

`filters: Array<Filter>`

The list of filters that are currently applied.


#### Example
```
import type {SearchableProps} from 'sonar';
import {Searchable} from 'sonar';

class MyPluginTable extends Component<{
  ...SearchableProps
}> {
  getRows() {
    const {rows, searchTerm, filters} = this.props;
    return rows.filter(row => {
      // filter rows for searchTerm and applied filters
    });
  }

  addFilter () {
    this.props.addFilter({
      type: 'include',
      key: '...',
      value: '...',
    });
  }

  render() {
    return <div>
      <Button onClick={this.addFilter}>Filter</Button>
      <Table rows={this.getRows()} />
    </div>
  }
}

export default SearchableTable = Searchable(MyPluginTable);
```
