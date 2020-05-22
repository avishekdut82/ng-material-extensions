# Angular Material Table Exporter

[![JavaScript Style Guide: Good Parts](https://img.shields.io/badge/code%20style-goodparts-brightgreen.svg?style=flat)](https://github.com/dwyl/goodparts "JavaScript The Good Parts")  [![Node version](https://img.shields.io/npm/v/mat-table-exporter.svg?style=flat)](https://www.npmjs.com/package/mat-table-exporter)  ![Total Downloads](https://img.shields.io/npm/dm/mat-table-exporter.svg)

This package is to make MatTable components exportable in ***excel, csv, txt*** and ***json*** formats. ***Pagination is also supported***. Applying MatTableExporter directive to your MatTable is enough to make it exportable. The directive uses different exporter services for different exporting types. You can also implement your own exporter and use it for your custom exporting requirements.

This project employs <a href="https://github.com/SheetJS/js-xlsx" target="_blank">xlsx sheetjs</a>, which is a great library and mature enough for the excel creation itself. In order to achieve a cross-browser file saving capability <a href="https://github.com/eligrey/FileSaver.js/" target="_blank">FileSaverjs</a> is employed.

The MatTableExporter directive inside this package is a cdk-table-exporter subtype and provides support for angular material's cdkTable.
cdk-table-exporter facilitates the common exporting related functionalities for CdkTable implementations abstracting the behavior that can change among different CdkTables.

&nbsp;

## Getting Started

### Angular Material Users

If you are employing angular material in your project. Install mat-table-exporter
```
npm install --save mat-table-exporter
```
NOTE: For the previous major versions of Angular (Angular 8 and older versions) install version 1.2.5 
```
npm install --save mat-table-exporter@1.2.5
```

After installing mat-table-exporter import MatTableExporterModule in your ngModule
```
import { MatTableExporterModule } from 'mat-table-exporter';
```
```
@NgModule({
  imports: [
    ...
    MatTableExporterModule
  ],
 ]})
```
&nbsp;

## Usage
### Angular Material Users

`matTableExporter` is the directive selector.
```html
<mat-table matTableExporter [dataSource]="dataSource" #exporter="matTableExporter">
```

```html
<button mat-button (click)="exporter.exportTable('csv')"></button>
```

&nbsp;

##### * Stackblitz demo: <a href="https://stackblitz.com/edit/mte-demo" target="_blank">mte-demo</a>.

##### * Stackblitz demo of custom exporter <a href="https://stackblitz.com/edit/mte-cex-demo" target="_blank">mte-cex-demo</a>.

&nbsp;

##API

### MatTableExporterDirective

| Input/Output | Property | Type | Description |
| --- | --- | --- | --- |
| `@Input` | hiddenColumns | `Array<number>` | (Optional) The indexes of the columns that are not wanted in the output file |
| `@Input` | exporter | `Exporter<Options>` | (Optional) The actual exporting implementation that defines the strategy to be applied to the rows extracted from MatTable. |
| `@Output` | exportStarted | `EventEmitter<void>` | (Optional) Event that's fired when the export started |
| `@Output` | exportCompleted | `EventEmitter<void>` | (Optional) Event that's fired when the export completed |

&nbsp;


| Method | Description    |
|----------|-------------|
| `exportTable(exportType?: ExportType, options?: Options)`   | Called to trigger the export of MatTable|
| `toggleRow(index: number)`   | Called to mark the row for selection export, if the requirement is to export only selected rows. Having no rows selected means export everything|

&nbsp;

### ExportType

```js
export enum ExportType {
  XLS = 'xls',
  XLSX = 'xlsx',
  CSV = 'csv',
  TXT = 'txt',
  JSON = 'json',
  OTHER = 'other'
}
```
&nbsp;

### Options


| Property | Type   | Description |
|----------|--------|-------------|
| fileName | `string` |(Optional) Name of the exported file|

&nbsp;

### ExcelOptions
ExcelOptions wraps the WritingOptions of sheetjs library. All other export types share the common Options interface. In the next releases, options will be enriched for the other export types.

| Property | Type   | Description |
|----------|--------|-------------|
| fileName | `string` |(Optional) Name of the exported file|
| type | `'base64', 'binary', 'buffer', 'file', 'array', 'string'` |(Optional) Output data encoding|
| bookSST | `boolean` |(Optional) Generate Shared String Table @default false|
| sheet | `string` |(Optional) Name of the exported sheet|
| compression | `boolean` |(Optional) Use ZIP compression for ZIP-based formats @default false|
| ignoreEC | `boolean` |(Optional) Suppress "number stored as text" errors in generated files @default true|
| Props | `Properties` |(Optional) Workbook properties like *Author, Title, Subject* etc.|
| columnWidths | `Array<number>` | (Optional) Column widths in maximum char  |
&nbsp;

## Contributing
This project is a library project inside ng-material-extensions angular workspace. If you are interested in the source code of this particular library you can get ready and build the project by applying the steps below:

1. Do ```npm install``` in ```ng-material-extensions``` directory
2. Do ```npm install``` in ```ng-material-extensions\projects\cdk-table-exporter``` directory
3. Do ```npm install``` in ```ng-material-extensions\projects\mat-table-exporter``` directory
4. Go to ```ng-material-extensions``` directory
5. Build both of the exporter packages:
```
ng build cdk-table-exporter
```
```
ng build mat-table-exporter
```
6. You can run the showcase application and see your changes in action. In ```ng-material-extensions``` run ```ng s -o```

## Licence

Apache-2.0