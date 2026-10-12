because it is structurally very similar to the `AssetDelegate`. It provides custom editing of the date field. We also hide both the log record's ID field and the `assetid` foreign key—there's no need to show which asset the log records are for because we are using master–detail, so the only log records that are visible are those that apply to the current asset. (We will see how the master–detail relationship is coded shortly.) The last difference is that we have set the last column to stretch to fill all the available space. The `QTableView.horizontalHeader()` method returns a `QHeaderView`, and this is what controls some aspects of the table view's columns, including their widths.

```
```
self.connect(self.assetView.selectionModel(),
    SIGNAL("currentRowChanged(QModelIndex,QModelIndex)"),
    self.assetChanged)

self.connect(addAssetButton, SIGNAL("clicked()"),
    self.addAsset)
```
```

If the user navigates to a different row we must update the log view to show the log records for the right asset. This is achieved by the first connection in conjunction with the `assetChanged()` method that we will review in a moment.

Every view has at least one selection model that is used to keep track of which items in the view's model (if any) are selected. We connect the view's selection model's `currentRowChanged()` signal so that we can update the log view depending on the current asset.

All the other connections are button-clicked connections like the second one shown here. We will cover all the methods the buttons connect to as we progress through this section.

```
```
self.assetChanged(self.assetView.currentIndex())
self.setMinimumWidth(650)
self.setWindowTitle("Asset Manager")
```
```

The initializer ends by calling the `assetChanged()` method with the asset view's current model index—this will result in the log view showing the relevant asset's records.

```
```
def assetChanged(self, index):
    if index.isValid():
        record = self.assetModel.record(index.row())
        id = record.value("id").toInt()[0]
        self.logModel.setFilter(QString("assetid = %1").arg(id))
    else:
        self.logModel.setFilter("assetid = -1")
        self.logModel.select()
        self.logView.horizontalHeader().setVisible(
                self.logModel.rowCount() > 0)
```
```