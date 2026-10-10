+   2. *stmt* variable contains the SELECT statement

+   2. Variable to be bound to the firstname, lastname and edlevel column

+   3. Sets auto commit off using *SQLSetConnectAttr* function.

+   4. Allocate statement handle using *SQLAllocHandle* function

+   5. Prepare the SELECT statement using *SQLPrepare* as the statement has parameter markers.

+   6. Bind *empno* variable to the statement using *SQLBindParameter* function.

+   7. Execute the statements using *SQLEecute* function for empno 50006.

+   8. Bind column 1 to variable firstname using *SQLBindCol* function.

+   9. Bind column 2 to variable lastname using *SQLBindCol* function.

+   10. Bind column 3 to variable edlevel using *SQLBindCol* function.

+   11. Fetch each row using *SQLFetch* function and display the results.

+   12. Commit the transaction using *SQLEndTrans* function.

+   13. Free the allocated statement handle using *SQLFreeHandle* function.

*Figure 5.31* shows the output of above code snippet

![](bbox=[0.16, 0.493, 0.84, 0.652])

*Figure 5.31* – Fetch employee information from the table

# **5.5.3.4.3 Deleting data**

*Listing 5.23* shows function *DeleteEmployeeInfo()*. It invokes *SQLExecDirect* to delete employee information.

```
/* Perform Delete operation */
int DeleteEmployeeInfo(SQLHANDLE hdbc)
{
  int funcRc = 0;
  SQLRETURN rc = SQL_SUCCESS;
```