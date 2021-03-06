# Table component with sorting and pagination for Angular
It is a forked version of [@cmglez10/ng-datatable](https://github.com/@cmglez10/ng-datatable) updated to Angular 7 with server and client pagination and record displaying.

## Usage example

AppModule.ts
```typescript
import {NgModule} from "@angular/core";
...
import {DataTableModule} from "angular-6-datatable";

@NgModule({
    imports: [
        ...
        DataTableModule
    ],
    ...
})
export class AppModule {

}
```

AppComponent.html
```html
<table class="table table-striped" [mfData]="data | dataFilter : filterQuery" #mf="mfDataTable" [mfRowsOnPage]="rowsOnPage"
                [(mfSortBy)]="sortBy" [(mfSortOrder)]="sortOrder" [mfActivePage]="activePage" (mfOnPageChange)="onPageChange($event)"
                [mfIsServerPagination]="true" [(mfAmountOfRows)]="itemsTotal" (mfSortOrderChange)="onSortOrder($event)">
                <thead>
                <tr>
                    <th style="width: 10%"></th>
                    <th style="width: 20%">
                        <mfDefaultSorter by="name">Name</mfDefaultSorter>
                    </th>
                    <th style="width: 40%">
                        <mfDefaultSorter by="email">Email</mfDefaultSorter>
                    </th>
                    <th style="width: 10%">
                        <mfDefaultSorter by="age">Age</mfDefaultSorter>
                    </th>
                    <th style="width: 20%">
                        <mfDefaultSorter [by]="sortByWordLength">City</mfDefaultSorter>
                    </th>
                </tr>
                </thead>
                <tbody>
                <tr *ngFor="let item of mf.data">
                    <td>
                        <button (click)="remove(item)" class="btn btn-danger">x</button>
                    </td>
                    <td>{{item.name}}</td>
                    <td>{{item.email}}</td>
                    <td class="text-right">{{item.age}}</td>
                    <td>{{item.city | uppercase}}</td>
                </tr>
                </tbody>
                <tfoot>
                <tr>
                    <td colspan="5">
                        <mfBootstrapPaginator [rowsOnPageSet]="[5,10,15]"></mfBootstrapPaginator>
                    </td>
                </tr>
                </tfoot>
            </table>
```

## API

### `mfData` directive

 - selector: `table[mfData]`
 - exportAs: `mfDataTable`
 - inputs
   - `mfData: any[]` - array of data to display in table
   - `mfRowsOnPage: number` - number of rows should be displayed on page (default: 1000)
   - `mfActivePage: number` - page number (default: 1)
   - `mfSortBy: any` - sort by parameter
   - `mfSortOrder: string` - sort order parameter, "asc" or "desc"
   - `mfIsServerPagination: boolean` -default value false
 - outputs
   - `mfSortByChange: any` - sort by parameter
   - `mfSortOrderChange: any` - sort order parameter
   - `mfOnPageChange: any` - page change parameter(rowsOnPage,activePage)
 
### `mfDefaultSorter` component

 - selector: `mfDefaultSorter`
 - inputs
   - `by: any` - specify how to sort data (argument for lodash function [_.sortBy ](https://lodash.com/docs#sortBy))
 
### `mfBootstrapPaginator` component
Displays buttons for changing current page and number of displayed rows using bootstrap template (css for bootstrap is required). If array length is smaller than current displayed rows on page then it doesn't show button for changing page. If array length is smaller than min value rowsOnPage then it doesn't show any buttons.

 - selector: `mfBootstrapPaginator`
 - inputs
   - `rowsOnPageSet: number` - specify values for buttons to change number of diplayed rows
