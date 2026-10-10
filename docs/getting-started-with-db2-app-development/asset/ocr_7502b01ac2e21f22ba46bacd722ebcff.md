A class implementing the Statement interface is used to execute an SQL statement which does not contain parameter markers. A Statement object is created with the createStatement method from a Connection object.

Table 4.4 shows the different methods applicable to the Statement object to execute a query.

| Method | Description |
| --- | --- |
| executeQuery | Use it when a result set is expected, for example, a SELECT statement. It returns a ResultSet object. |
| executeUpdate | Use it for updates of database contents, for example, INSERT, UPDATE, and DELETE. It returns an integer with the number of rows affected. |
| execute | Use it when you don’t know until runtime whether the statement executed is a SELECT or an UPDATE statement. It returns true if the result of the SQL is a result set, false if it’s an update count. Use this method in conjunction with getResultSet or getUpdateCount methods. |

# Table 4.4 - Methods of the Statement object

Listing 4.4 provides a code snippet that illustrates the use of a Statement object, and the executeQuery method.

```
```
(1) Statement stmt = con.createStatement();
(2) ResultSet rs = stmt.executeQuery
    ("SELECT EMPNO, FIRSTNAME, LASTNAME " +
     " FROM EMPLOYEE " +
     " WHERE SALARY > 80000" );
(3) while ( rs.next() ) {
       System.out.println("Empno = " + rs.getString(1) +
              " Full name = " + rs.getString(2) +
              " " + rs.getString(3));
   }
(4) rs.close();
(5) stmt.close();
(6) con.close();
} catch (Exception e) {
   e.printStackTrace();
}
} }
```
```

# Listing 4.4 - Statement object: Performing a SELECT with executeQuery