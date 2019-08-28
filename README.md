# Venoid Admin Table Component

Table component for your administration provides you good options how to load and render your data in a simple table.

![screenshot-example](https://bitbucket.org/venoid/admin-table/raw/a8d03e2292c2e1757405fee426075b8f9439fd4a/images/example.png)

## Props
| Props         | Type    | Default   |                                      |
|---------------|---------|-----------|--------------------------------------|
| table-columns | Array   | undefined | Array of objects with options        |
| table-data    | Array   | undefined | Array with your data                 |
| is-loading    | Boolean | false     | When true, loading animation appears |
| paginated     | Boolean | false     | When true, pagination appears        |
| totalDataCount | Number | null     | Total count of your data             |
| currentPage   | Number  | 1         | Number of the current page           |
| perPageOptions   | Array  | [{value: '5', label: 5}, {value: '10', label: 10}, {value: '15', label: 15}, {value: '20', label: 20}]         | Define your own select box with per page options |

#### table-columns options
```
{
  type: 'string' // Enum['id', 'number', 'string ],
  label: 'Name'  // String,
  field: (row) => row.name //Render function for data,
  width: '60' // String
}
```

## Demo
To see demo run a project:

1. Install npm dependencies
2. Run with `npm run serve` / `yarn serve`
