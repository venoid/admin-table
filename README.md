# Venoid Admin Table Component

[![npm](https://img.shields.io/npm/v/@venoid/admin-table?color=green)](https://www.npmjs.com/package/@venoid/admin-table)
![npm bundle size (scoped)](https://img.shields.io/bundlephobia/min/@venoid/admin-table)

Table component for your administration provides you good options how to load and render your data in a simple table.

![screenshot-example](https://raw.githubusercontent.com/venoid/admin-table/master/images/example.png)

## New features
- Sortable columns
- Backend sorting. Sort data by yourself on backend.

## Props
| Props         | Type    | Default   |                                      |
|---------------|---------|-----------|--------------------------------------|
| table-columns | Array   | undefined | Array of objects with [options](#table-column-options)        |
| table-data    | Array   | undefined | Array with your data                 |
| is-loading    | Boolean | false     | When true, loading animation appears |
| paginated     | Boolean | false     | When true, pagination appears        |
| is-simple-pagination     | Boolean | false     | When true, simple pagination appears - just arrows and current bulk        |
| default-sort | Array | [] | Has two elements - field and sort type        |
| total-data-count | Number | null     | Total count of your data (if paginated is true) |
| current-page   | Number  | 1         | Number of the current page (if paginated is true) |
| per-page-options   | Array  | [{value: '5', label: 5}, {value: '10', label: 10}, {value: '15', label: 15}, {value: '20', label: 20}]         | Define your own select box with per page options (if paginated is true) |
| backend-sorting | Boolean | false | If true handle sorting on yourself see [sort event](##events) |
| error-message | String | null | Message which displays when there are no data in a table |

#### table-column options
```
{
  type: 'string' // Enum['id', 'number', 'string ],
  label: 'Name'  // String,
  fieldName: 'name' // name of the property you want to render - needed if using sortable!
  field: (row) => row.name //Render function for data,
  width: '60' // String,
  sortable: true // the column will be sortable
}
```

## Events
| Events        | payload    | Description   |
|---------------|---------|-----------|
| pagination-change   | object with currentPage and perPage | Triggers when something in paginator changes. |
| sort                | object with field and order | Triggers when clicked on sortable column |

## Demo
To see demo run a project:

1. Install npm dependencies
2. Run with `npm run serve` / `yarn serve`
