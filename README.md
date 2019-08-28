# Venoid Admin Table Component

Table component for your administration provides you good options how to load and render your data in a simple table.

![screenshot-example](https://bitbucket.org/venoid/admin-table/raw/a8d03e2292c2e1757405fee426075b8f9439fd4a/images/example.png)

## Props
| Props         | Type    | Default   |                                      |
|---------------|---------|-----------|--------------------------------------|
| table-columns | Array   | undefined | Array of objects with options        |
| table-data    | Array   | undefined | Array with your data                 |
| is-loading    | Boolean | false     | When true, loading animation appears |

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
