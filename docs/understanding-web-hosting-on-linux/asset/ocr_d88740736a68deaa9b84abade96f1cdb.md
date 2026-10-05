As you learned in the last chapter, the init method of a servlet is called the first time the servlet is loaded. All subsequent requests will not cause the init method to execute. The JDBC connection object created in the init method is a global variable that will be shared by all requestors. Each user's request to the JDBCBasics servlet will be handled with its doGet method.

After the obligatory statements for setting the content type, getting an output stream, and dumping the opening HTML tags, the doGet method is ready to specify the SQL statement by creating a Statement

```
Statement stmtt = con.createStatement();
```

This object is an interface class whose executeQuery function enables SQL statements to funnel through the JDBC driver to your host RDB:

```
ResultSet rs = stmt.executeQuery(
  "SELECT CUSTOM, LSTNAM, INIT, STREET," +
  "CITY, STATE, ZIPCOD, CDTLMT, " +
  "CHCGOD, BALDUE, CDTDUE " +
  "FROM QWIWS.QCUSTCDT");
```

When that SQL query function completes, it returns a set of records in the form of a ResultSet object. Table 8.5 shows all the functions of the JDBC Statement class. One particularly noteworthy function, executeUpdate, is used for executing an SQL. INSERT, UPDATE, or DELETE statement.