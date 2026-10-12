```
if self.assetView.currentIndex().isValid() else 0

    QSqlDatabase.database().transaction()
    self.assetModel.insertRow(index)
    index = self.assetModel.index(row, NAME)
    self.assetView.setCurrentIndex(index)

    assetid = 1
    query = QSqlQuery()
    query.exec("SELECT MAX(id) FROM assets")
    if query.next():
        assetid = query.value(0).toInt()[0]
    query.prepare("INSERT INTO logs (assetid, date, actionid) "
                  "VALUES (:assetid, :date, :actionid)")
    query.bindValue(":assetid", QVariant(assetid + 1))
    query.bindValue(":date", QVariant(QDate.currentDate()))
    query.bindValue(":actionid", QVariant(ACQUIRED))
    query.exec()
    QSqlDatabase.database().commit()
    self.assetView.edit(index)
```

When the user adds a new asset we want to create a new log record for the asset with its action set to “Acquired”. Naturally, we want either both of these records created, or, if something goes wrong, neither, and to do this we must use a transaction.

We begin by initiating a transaction. Then we insert a new row and make it the current one in the asset view. If this is the very first asset, its ID will be 1, but if there are other assets, its ID will be one more than the highest asset ID. We execute a query to find the current highest asset ID and then we use a prepared query (so that we don't have to worry about quoting, to insert a new record into the logs table. Once the new record has gone into the logs table, we commit the transaction. Now we will have one log record for the new asset, with an action of “Acquired”, and a new blank asset record. Finally, we initiate editing on the new asset's name field.

We will finish reviewing the main form by looking at the deleteAsset() method. The method is slightly involved, so we will look at it in three parts.

```
def deleteAsset(self):
    index = self.assetView.currentIndex()
    if not index.isValid():
        return

    QSqlDatabase.database().transaction()
    record = self.assetModel.record(index, row())
    assetid = record.value(ID).toInt()[0]
    logrecords = 1

    query = QSqlQuery(QString("SELECT COUNT(*) FROM logs "
                              "WHERE assetid = %1").arg(assetid))
```