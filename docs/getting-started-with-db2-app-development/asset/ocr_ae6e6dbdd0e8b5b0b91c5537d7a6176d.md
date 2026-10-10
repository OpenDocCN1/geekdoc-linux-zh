# **3.3.11 Calling stored procedures**

The following code snippets illustrated in *Listings 3.5, 3.6 and 3.7* show how to CALL stored procedures from a CLI/ODBC, VB.NET, and Java program respectively.

```
```
SQLCHAR *stmt = {SQLCHAR *}
*CALL MEDIAN_RESULT_SET( ? )" ;
SQLDOUBLE  sal = 20000.0;  /* Bound to parameter marker in stmt */
SQLINTEGER salind = 0;     /* Indicator variable for sal */

sqlrc = SQLPrepare(hstmt, stmt, SQL_NTS);
sqlrc = SQLBindParameter(hstmt, 1, SQL_PARAM_OUTPUT,
SQL_C_DOUBLE, SQL_DOUBLE, 0, 0, &sal, 0, &salind);
SQLExecute(hstmt);

if (salind == SQL_NULL_DATA)
  printf("Median Salary = NULL\n");
else
  printf("Median Salary = %.2f\n\n", sal );

/* Get first result set */
  sqlrc = StmtResultPrint(hstmt);
/* Check for another result set */
  sqlrc = SQLMoreResults(hstmt);
if (sqlrc == SQL_SUCCESS) {
/* There is another result set */
  sqlrc = StmtResultPrint(hstmt);
}
```
```

**Listing 3.5 - Example calling a stored procedure from a CLI/ODBC application**

For more details, see the DB2 sample file: sqllib/samples/sqlproc/resultset.c

```
```
Try
    ' Create a DB2Command to run the stored procedure
    Dim procName As String = "TRUNC_DEMO"
    Dim cmd As DB2Command = conn.CreateCommand()
    Dim parm As DB2Parameter

    cmd.CommandType = CommandType.StoredProcedure
    cmd.CommandText = procName

    ' Register the output parameters for the DB2Command
    parm = cmd.Parameters.Add("v_lastname", DB2Type.Varchar)
    parm.Direction = ParameterDirection.Output
```
```