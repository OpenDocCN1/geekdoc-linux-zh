**Note:**
For more details on namespaces refer to
http://publib.boulder.ibm.com/infocenter/db2luw/v9r7/index.jsp?topic=com.ibm.swg.im.dbcllient.adonet.ref.doc/IBMDataDB2Namespace.html

# 6.2.1.1 Connection

The **Connection** object is used to connect to a database and control the transactions in ADO.NET. Each of the three data providers mentioned earlier has their own **Connection Object** (**DB2Connection**, **OleDbConnection**, and **OdbcConnection**). The **Connection** object has a public property **ConnectionString**, which is required for establishing a connection to the database. **ConnectionString** requires the database name and other parameters such as user ID and password. For example:

```
connection.ConnectionString = "Database=Sample";
```

The **ConnectionString** property can be set through the **Connection** object constructor, as shown in *Table 6.2 below*.

| Provider | Example |
| :--- | :--- |
| IBM Data Server Provider for .NET | `DB2Connection connection = new DB2Connection("Database=SAMPLE");` |
| OLE DB .NET Data Provider | `OleDbConnection connection = new OleDbConnection("Provider=IBMADDB2;" + "Data Source=sample;UID=userid;PWD=password;");` |
| ODBC.NET Data Provider | `OdbcConnection connection = new OdbcConnection("DSN=sample;UID=userid;PWD=password;");` |

**Table 6.2 - Connection string depending on the data provider used**

*Table 6.3* describes the Connection object public methods.

| Method name | Description | Example |
| :--- | :--- | :--- |
| **Open** | This opens a database connection as specified in a connection_string. Connections can be opened by explicitly calling the Open method on the connection or by implicitly using a | `connection.Open();` |