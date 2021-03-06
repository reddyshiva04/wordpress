# Instructions on Sorting

1. Place an icon on the column header onclick to a function

```html
<i (click)="sortString(customers, 'lastName', lastNameSortStatus)" class="icon sort"></i>          
```

2. Place a sortstatus object that indicates how the column is currently sorted. Put this in the component.ts
```typescript
  lastNameSortStatus = {order : -1};
```

## Create the sort functions
Place the above functions in a common library ts file to enable reuse across different components.

shared/sortFunc.ts
```typescript
export function sortString(arrayToSort, field, fieldOrder) {
    if(fieldOrder.order==-1 || fieldOrder.order==0) { // sort Asc
        fieldOrder.order = 1;
    } else if(fieldOrder.order == 1) { // sort desc
        fieldOrder.order = -1;
    }
    arrayToSort.sort((a,b) : number => {
        if(a[field]==null) return -1;
        if(b[field]==null) return 1;
        if(a[field].toUpperCase() < b[field].toUpperCase()) return -fieldOrder.order;
        if(a[field].toUpperCase() > b[field].toUpperCase()) return fieldOrder.order;
        return 0;
    });
}

export function sortNumber(arrayToSort, field, fieldOrder) {
    if(fieldOrder.order==-1 || fieldOrder.order==0) { // sort Asc
      fieldOrder.order = 1;
    } else if(fieldOrder.order == 1) { // sort desc
      fieldOrder.order = -1;
    }
    arrayToSort.sort((a,b) : number => {
      if(a[field]==null) return -1;
      if(b[field]==null) return 1;
      if(a[field] < b[field]) return -fieldOrder.order;
      if(a[field] > b[field]) return fieldOrder.order;
      return 0;
    });
}
```

2. Import the function into the components
```typescript
import * as sortFunc from '../shared/sortFunc';
```
3. Assign the functions to member variables so they can be used by the html template.
```typescript
  // imported functions
  sortString=sortFunc.sortString;
  sortNumber=sortFunc.sortNumber;
```
