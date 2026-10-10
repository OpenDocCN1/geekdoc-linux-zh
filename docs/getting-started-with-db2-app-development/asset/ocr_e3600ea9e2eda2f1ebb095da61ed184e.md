The above code snippets are part of the script `param.py` included in the exercise files accompanying this book. In addition to SELECT statements, the script also contains an example of executing an UPDATE statement with parameter markers. If you want to test the code snippets, you can modify the user ID and password in the script appropriately and run it as:

`python param.py`

The result of executing the script `param.py` is illustrated in *Figure 10.7*.

![](bbox=[0.155, 0.35, 0.85, 0.51])

Figure 10.7 - Executing the script `param.py`

# 10.3.5 Call a stored procedure

To call a stored procedure from a Python application, you can follow the steps below:

+   1. Create a database connection object by connecting to the database with the `ibm_db.connect` function.
+   2. Invoke the stored procedure by calling the function `ibm_db.callproc`, which returns a tuple with the first item as the statement object and the rest of items as the modified copy of the parameters. The statement object contains the result sets returned from a stored procedure if there is any, while the OUT and INOUT parameters are replaced with possibly new values, and the input parameters are left unchanged. If there is multiple result sets, you can call `ibm_db.next_result` method by passing the original statement resource as the first argument, for example `stmt1 = ibm_db.next_result(stmt)`, to move to the next result set.

The syntax of `ibm_db.callproc` is:

`tuple ibm_db.callproc ( IBM_DBConnection connection, string procname, [tuple parameters] )`

*Table 10.7* describes the parameters of `ibm_db.callproc`