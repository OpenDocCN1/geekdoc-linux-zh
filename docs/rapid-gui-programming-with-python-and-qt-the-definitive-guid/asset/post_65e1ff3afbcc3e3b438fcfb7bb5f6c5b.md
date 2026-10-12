
is to ensure that we either remove or escape unacceptable characters, but PyQt provides a better alternative: prepared queries.

There are two widely used forms of syntax for prepared queries, one based on the ODBC place holder approach, and the other based on the Oracle named variable approach. PyQt supports both, converting from one to the other behind the scenes if necessary, so that both work no matter what the underlying database is.

```python
query.prepare("INSERT INTO calls (caller, starttime, endtime, "
              "topic, outcomeid) VALUES (?, ?, ?, ?, ?, ?)")
for name, start, end, topic, outcomeid in data:
    query.addBindValue(QVariant(Qstring(name)))
    query.addBindValue(QVariant(start))      # QDateTime
    query.addBindValue(QVariant(end))        # QDateTime
    query.addBindValue(QVariant(Qstring(topic)))
    query.addBindValue(QVariant(outcomeid))  # int
query.exec_()
```

This example uses the ODBC syntax. One benefit of using place holders is that PyQt takes care of the quoting issues, so we don’t have to worry about what our data contains, as long as the types we pass are appropriate for the fields they will populate.

```python
query.prepare("INSERT INTO calls (caller, starttime, endtime, "
              "topic, outcomeid) VALUES (:caller, :starttime, "
              ":endtime, :topic, :outcomeid)")
for name, start, end, topic, outcomeid in data:
    query.bindValue(":caller", QVariant(Qstring(name)))
    query.bindValue(":starttime", QVariant(start))
    query.bindValue(":endtime", QVariant(end))
    query.bindValue(":topic", QVariant(Qstring(topic)))
    query.bindValue(":outcomeid", QVariant(outcomeid))
query.exec_()
```

This second example performs the same work as the first, but uses Oracle-style named variables. PyQt also supports a couple of other variations of prepared query syntax, but they don’t add anything to what we can do with the two forms of syntax shown earlier. Prepared queries can improve performance on databases that support them, and make no difference on those that don’t.

Prepared queries can also be used to call stored procedures, but we will not cover them because support for them is neither universal nor uniform. For example, not all databases support stored procedures, and the syntax for calling them and for retrieving Qut values is different from database to database. Also, stored procedures that return values are not fully supported.

We can use QSqlQuery to execute any arbitrary SQL statement. For example:

```python
query.exec_("DELETE FROM calls WHERE id = 12")
```

After a query has executed we can check for errors by calling QsqlQuery.isActive(); if this returns False an error occurred and the error message is available as a QString by calling QsqlQuery.lastError().text().

If we perform a query that may affect a number of rows, such as a DELETE or UPDATE whose WHERE clause might select more than one record, we can call QsqlQuery.numRowsAffected(); it returns -1 on error.

We can find out whether the underlying database supports various features such as transactions and BLOBs (Binary Large Objects) by accessing the driver and calling hasFeature(). For example:

```python
driver = QSqlDatabase.database().driver()
if driver.hasFeature(QsqlDriver.Transactions):
    print "Can commit and rollback"
```

When we use QsqlQuery we can initiate a transaction by calling QsqlDatabase.database().transaction(), and then either QsqlDatabase.database().commit() or QsqlDatabase.database().rollback().

We will conclude our coverage of QsqlQuery by looking at how to use it to execute SELECT statements, and how to iterate over the resultant records.

```python
DATETIME_FORMAT = "yyyy-MM-dd hh:mm"
ID, CALLER, STARTTIME, ENDTIME, TOPIC, OUTCOMEID = range(6)

query.exec_("SELECT id, caller, starttime, endtime, topic, "
            "outcomeid FROM calls ORDER by starttime")
while query.next():
    id = query.value(ID).toInt()[0]
    caller = unicode(query.value(CALLER).toString())
    starttime = unicode(query.value(STARTTIME).toDateTime() \
                .toString(DATETIME_FORMAT))
    endtime = unicode(query.value(ENDTIME).toDateTime() \
                .toString(DATETIME_FORMAT))
    topic = unicode(query.value(TOPIC).toString())
    outcomeid = query.value(OUTCOMEID).toInt()[0]
    subquery = QsqlQuery("SELECT name FROM outcomes "
                     "WHERE id = %d" % outcomeid)
    outcome = "invalid foreign key"
    if subquery.next():
        outcome = unicode(subquery.value(0).toString())
    print "%02d: %s - %s %%s [%%s]" % (id, caller, starttime, endtime, topic, outcome)
```

When we execute a SELECT statement, we can iterate over the result set using methods such as QsqlQuery.next(), QsqlQuery.previous(), and QsqlQuery.seek(). Immediately after a successful SELECT, isActive() will return True but the inter-nal record pointer will not be referring to a valid record. Each of the navigation methods returns True if the query’s internal record pointer was successfully moved onto a valid record; this is why we call QSqlQuery.next() before accessing the first record. They return False if an error occurred or if they pass the last (or first) record.

When navigating large result sets, providing we only use next(), or only seek() forward, we can call QSqlQuery.setForwardOnly(True). This can significantly improve performance or reduce memory overhead, or both, with some databases.

The QSqlQuery.value() method takes an index position argument, based on the order of the field names given in the SELECT statement. For this reason, using SELECT * is not recommended because in that case, we don’t know what the order of the fields is. Each field is returned as a QVariant and must therefore be converted to the proper type. In the case of the date/times, we first convert them from QVariant to QDateTime, then to QString, and finally to unicode, ready to be printed on the console.

We used an additional query to look up the name of the outcome from its ID, giving error text if the database does not have relational integrity. For a large dataset, it would have been more efficient to use a prepared query for the subquery.

We can use QsqlQuery to do all the database work we want, but using PyQt’s SQL models is much easier for GUI programming, and it does not prevent us from using QsqlQuery when the need arises.

## Selected QSqlQuery Methods

| Syntax | Description |
| :--- | :--- |
| q.addBindValue(v) | Adds QVariant v as the next variable when using position value binding in QSqlQuery q |
| q.bindValue(p, v) | Sets QVariant v as the value for the string p place holder when using place holder value binding in QSqlQuery q |
| q.boundValue(p) | Returns the QVariant value for the string p place holder in QSqlQuery q |
| q.driver() | Returns the QSqlDriver associated with QSqlQuery q. The QSqlDriver class provides hasFeature() to report which features the underlying database supports. |
| q.exec_(s) | Executes the SQL query in string s on QSqlQuery q |
| q.first() | Navigates to the first record in QSqlQuery q's result set after a SELECT query has been executed |
| q.isActive() | Returns True if the query is "active"—for example, after executing a SELECT query |
| q.isValid() | Returns True if the query is positioned on a valid record; after a SELECT query this will be True only if isActive() is True and a record has been navigated to |
| q.last() | Navigates to the last record in QSqlQuery q's result set after a SELECT query has been executed |
| q.lastError() | Returns a QSqlError object; this provides an error-String() method |
| q.next() | Navigates to the next record in QSqlQuery q's result set after a SELECT query has been executed. This is the only method needed to iterate forward over a result set. |
| q.numRowsAffected() | Returns the number of rows affected by the SQL query just executed, providing it was not a SELECT, and providing the underlying database supports this feature |
| q.prepare(s) | Prepares the query in string s ready for q to execute it |
| q.previous() | Navigates to the previous record in QSqlQuery q's result set after a SELECT query has been executed |
| q.record() | Returns a QSqlRecord object containing QSqlQuery q's current record, if any; using QSqlQuery.value() with a field index argument is usually more convenient |
| q.size() | Returns the number of rows in the SELECT result set, or -1 if a SELECT was not executed or if the underlying database does not support this feature |
| q.value(i) | Returns the QVariant value for field index int i in the current record, if there is one |

### Using Database Form Views

One of the easiest user interfaces you can provide for database data is a form that displays the fields from a single record at a time. In this section we will develop an application that uses such a form, initially a simplified version of the phone log database introduced in the preceding section, and then the full version which includes the foreign key field.

The examples presented in this section depend on the QtDataWidgetMapper class introduced with Qt 4.2. The next section’s example uses SQL table models and QTableView, and can be used with Qt 4.1 or later.

![](img/9bfe0a027fcc8793bb087287001100dd_465_0.png)

The simplified application is shown in Figure 15.2, and its source code is in chapp15/phoneLog.pyw; the full version is in chapp15/phoneLog-fk.pyw. When these applications are run for the very first time they create a database of fake records which they then use on subsequent runs. Generating these records using Qt’s built-in SQLite is fast on Linux but very slow on some Windows machines. (A splash screen is used to disguise the slowness.)

The simplified application has a single table, calls, and no foreign key field. The form is represented by the PhoneLogDlg class. The initializer is quite long,
