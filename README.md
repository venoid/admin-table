# Venoid Admin Table Component

[![npm](https://img.shields.io/npm/v/@venoid/admin-table?color=green)](https://www.npmjs.com/package/@venoid/admin-table)
![npm bundle size (scoped)](https://img.shields.io/bundlephobia/min/@venoid/admin-table)

Table component for your administration provides you good options how to load and render your data in a simple table.

![screenshot-example](https://camo.githubusercontent.com/163090216f541ff54c665ce6849c6004d88120ae/68747470733a2f2f6269746275636b65742e6f72672f76656e6f69642f61646d696e2d7461626c652f7261772f613864303365323239326332653137353734303566656534323630373562386639343339666434612f696d616765732f6578616d706c652e706e67)

## Props
| Props         | Type    | Default   |                                      |
|---------------|---------|-----------|--------------------------------------|
| table-columns | Array   | undefined | Array of objects with [options](#table-column-options)        |
| table-data    | Array   | undefined | Array with your data                 |
| is-loading    | Boolean | false     | When true, loading animation appears |
| paginated     | Boolean | false     | When true, pagination appears        |
| total-data-count | Number | null     | Total count of your data (if paginated is true) |
| current-page   | Number  | 1         | Number of the current page (if paginated is true) |
| per-page-options   | Array  | [{value: '5', label: 5}, {value: '10', label: 10}, {value: '15', label: 15}, {value: '20', label: 20}]         | Define your own select box with per page options (if paginated is true) |
| error-message | String | null | Message which displays when there are no data in a table |

#### table-column options
```
{
  type: 'string' // Enum['id', 'number', 'string ],
  label: 'Name'  // String,
  field: (row) => row.name //Render function for data,
  width: '60' // String
}
```

## Events
| Events        | payload    | Description   |
|---------------|---------|-----------|
| pagination-change   | object with currentPage and perPage | Triggers when something in paginator changes. |

## Demo
To see demo run a project:

1. Install npm dependencies
2. Run with `npm run serve` / `yarn serve`
