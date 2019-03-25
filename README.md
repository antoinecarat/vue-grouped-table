# vue-grouped-table

## Usage

### Install

```bash
npm install @acarat/vue-grouped-table
```

### Import the component

```js
import { GroupedTable } from "@acarat/vue-grouped-table";
```

### Use the component in your Vue project

```html
<GroupedTable :headers="[
                          'city',
                          'name',
                          'age',
                          'genre'
                        ]"
              :entries="[
                          { city: 'Dublin', name: 'Antoine', age: 23, genre: 'M' },
                          { city: 'Dublin', name: 'Margaux', age: 24, genre: 'F' },
                          { city: 'Nantes', name: 'Mattis', age: 23, genre: 'M' },
                          { city: 'Nantes', name: 'Hugo', age: 24, genre: 'M' },
                          { city: 'Nantes', name: 'Laurie', age: 23, genre: 'F' },
                          { city: 'Marrakech', name: 'Amr', age: 25, genre: 'M' }
                        ]"
/>
```

## Props

### headers

headers must be an Array containing the headers of the table, ie the properties by which the data is grouped.

### entries

entries is the raw data itself and must be an Array of Object.