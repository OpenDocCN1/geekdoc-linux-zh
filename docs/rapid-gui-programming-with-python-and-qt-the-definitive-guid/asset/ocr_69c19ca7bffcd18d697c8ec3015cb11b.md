# **Table 15.1** Selected QSqlQuery Methods

| Syntax | Description |
| :--- | :--- |
| q.addBindValue(v) | Adds QVarint v as the next variable when using position value binding in QSqlQuery q |
| q.bindValue(p, v) | Sets QVarint v as the value for the string p place holder when using place holder value binding in QSqlQuery q |
| q.boundValue(p) | Returns the QVarint value for the string p place holder in QSqlQuery q |
| q.driver() | Returns the QSqlDriver associated with QSqlQuery q. The QSqlDriver class provides hasFeature() to report which features the underlying database supports. |
| q.exec (s) | Executes the SQL query in string s on QSqlQuery q |
| q.first() | Navigates to the first record in QSqlQuery q's result set after a SELECT query has been executed |
| q.isActive() | Returns True if the query is "active"—for example, after executing a SELECT query |
| q.isValid() | Returns True if the query is positioned on a valid record; after a SELECT query this will be True only if isActive() is True and a record has been navigated to |
| q.last() | Navigates to the last record in QSqlQuery q's result set after a SELECT query has been executed |
| q.lastError() | Returns a QSqlError object; this provides an error-String() method |
| q.next() | Navigates to the next record in QSqlQuery q's result set after a SELECT query has been executed. This is the only method needed to iterate forward over a result set. |
| q.numRows-Affected() | Returns the number of rows affected by the SQL query just executed, providing it was not a SELECT, and providing the underlying database supports this feature |
| q.prepare(s) | Prepares the query in string s ready for q to execute it |
| q.previous() | Navigates to the previous record in QSqlQuery q's result set after a SELECT query has been executed |
| q.record() | Returns a QSqlRecord object containing QSqlQuery q's current record, if any; using QSqlQuery.value() with a field index argument is usually more convenient |
| q.size() | Returns the number of rows in the SELECT result set, or -1 if a SELECT was not executed or if the underlying database does not support this feature |
| q.value(i) | Returns the QVarint value for field index int i in the current record, if there is one |