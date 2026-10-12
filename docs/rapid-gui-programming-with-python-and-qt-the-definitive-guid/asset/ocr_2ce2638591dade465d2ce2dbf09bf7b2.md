nal record pointer will not be referring to a valid record. Each of the navigation methods returns True if the query’s internal record pointer was successfully moved onto a valid record; this is why we call QSqlQuery.next() before accessing the first record. They return False if an error occurred or if they pass the last (or first) record.

When navigating large result sets, providing we only use next(), or only seek() forward, we can call QSqlQuery.setForwardOnly(True). This can significantly improve performance or reduce memory overhead, or both, with some databases.

The QSqlQuery.value() method takes an index position argument, based on the order of the field names given in the SELECT statement. For this reason, using SELECT * is not recommended because in that case, we don’t know what the order of the fields is. Each field is returned as a QVariant and must therefore be converted to the proper type. In the case of the date/times, we first convert them from QVariant to QDateTime, then to QString, and finally to unicode, ready to be printed on the console.

We used an additional query to look up the name of the outcome from its ID, giving error text if the database does not have relational integrity. For a large dataset, it would have been more efficient to use a prepared query for the subquery.

We can use QsqlQuery to do all the database work we want, but using PyQt’s SQL models is much easier for GUI programming, and it does not prevent us from using QsqlQuery when the need arises.

# # Using Database Form Views

One of the easiest user interfaces you can provide for database data is a form that displays the fields from a single record at a time. In this section we will develop an application that uses such a form, initially a simplified version of the phone log database introduced in the preceding section, and then the full version which includes the foreign key field.

The examples presented in this section depend on the QtDataWidgetMapper class introduced with Qt 4.2. The next section’s example uses SQL table models and QTableView, and can be used with Qt 4.1 or later.

![](bbox=[0.88, 0.63, 0.95, 0.71])

The simplified application is shown in Figure 15.2, and its source code is in chapp15/phoneLog.pyw; the full version is in chapp15/phoneLog-fk.pyw. When these applications are run for the very first time they create a database of fake records which they then use on subsequent runs. Generating these records using Qt’s built-in SQLite is fast on Linux but very slow on some Windows machines. (A splash screen is used to disguise the slowness.)

The simplified application has a single table, calls, and no foreign key field. The form is represented by the PhoneLogDlg class. The initializer is quite long,