# How to update a cell value in the selected row of Flutter DataTable (SfDataGrid)?

In this article, we will show you how to update a cell value in the selected row of [Flutter DataTable](https://www.syncfusion.com/flutter-widgets/flutter-datagrid).

Initialize the [SfDataGrid](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/SfDataGrid-class.html) with the necessary properties. You can access the currently selected row using [DataGridController.selectedRow](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridController/selectedRow.html). The row index is determined using [DataGridSource.rows](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSource/rows.html), which identifies the position of the selected row. The [getCells()](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridRow/getCells.html) method returns a list of cells in the row, allowing you to update specific cells (e.g., ID and Name). After modifying a cell’s value, call the [notifyDataSourceListeners](https://pub.dev/documentation/syncfusion_flutter_datagrid/latest/datagrid/DataGridSourceChangeNotifier/notifyDataSourceListeners.html) method with the RowColumnIndex argument to specify the corresponding row and column index. This ensures that only the updated cell is refreshed in the DataGrid.

```dart
TextButton(
    onPressed: () {
    if (dataGridController.selectedRow != null) {
        final selectedRow = dataGridController.selectedRow!;
        final rowIndex =
            employeeDataSource._employeeData.indexOf(selectedRow);

        if (rowIndex >= 0) {
        final List<DataGridCell> cells =
            employeeDataSource._employeeData[rowIndex].getCells();

        // Find the index of the 'id' column in the row.
        final int colIndex =
            cells.indexWhere((cell) => cell.columnName == 'id');
        if (colIndex != -1) {
            employees[rowIndex].id = 100;
            employeeDataSource._employeeData[rowIndex]
                    .getCells()[colIndex] =
                const DataGridCell<int>(columnName: 'id', value: 100);
            employeeDataSource.updateDataGridSource(
                rowColumnIndex: RowColumnIndex(rowIndex, colIndex));
          }
        }
    }
    },
    child: const Text('Cell value')
),
```

You can download this example on [GitHub](https://github.com/SyncfusionExamples/How-to-update-a-cell-value-in-the-selected-row-of-Flutter-DataTable).