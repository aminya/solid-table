# Solid Table

![CI](https://github.com/aminya/solid-simple-table/workflows/CI/badge.svg)

Solid Table is an efficient reactive table component that gives you freedom.

![Simple table demo](images/2020/12/simple-table-demo.png)

## Installation

      npm install --save solid-simple-table

## Usage

```js
import { render } from "solid-js/web"

import { SimpleTable } from "solid-simple-table"
import type { SortDirection } from "solid-simple-table"

const rows = [
  { file: "C:/a", message: "Lorem ipsum dolor sit amet, consectetur", severity: "error" },
  { file: "C:/b", message: "Vivamus tincidunt ligula ut ligula laoreet faucibus", severity: "warning" },
  { file: "C:/c", message: "Proin tincidunt justo nulla, sit amet accumsan lectus pretium vel", severity: "info" },
  { file: "C:/d", message: "Cras faucibus eget ante ut consectetur", severity: "error" },
]

function MyTable() {
  return <SimpleTable rows={rows} />
}

render(() => <MyTable />, document.getElementById("app"))
```

For other examples see the demo folder.

## API

```ts

<SimpleTable
  // row
  rows: Array<Row<K, V>>

  // Optional props:

  // columns
  columns?: Array<Column<K, V>>

  // renderers
  headerRenderer?(column: Column): string | Renderable
  bodyRenderer?(row: Row, columnKey: K): string | Renderable

  // styles
  style?: AnyObject
  className?: string

  // sort options
  defaultSortDirection?: NonNullSortDirection<K>
  rowSorter?(rows: Array<Row>, sortDirection: NonNullSortDirection<K>): Array<Row>

  /** a function that takes row and returns string unique key for that row */
  rowKey?(row: Row): string
/>;

```

In which:

```ts
// util types
export type AnyObject = Record<string, any>
export type Renderable = any

// row and column types
export type Key = string
export type Row<K extends Key = string, V = any> = Record<K, V>

export type Column<K extends Key = string, V = any> = {
  key: K
  label?: string
  sortable?: boolean
  onClick?(e: MouseEvent, row: Row<K, V>): void
}

/** Sort direction.
  It is a tuple:
  @columnKey is the key used for sorting
  @type is the direction of the sort
*/
export type NonNullSortDirection<K = Key> = [columnKey: K, type: "asc" | "desc"]
export type SortDirection<K = Key> = NonNullSortDirection<K> | [columnKey: null, type: null]
```

## License

This package is licensed under the terms of MIT License. It was converted from [sb-react-table](https://github.com/steelbrain/react-table/tree/2f8472960a77ca6cf2444c392697772716195bf4).
