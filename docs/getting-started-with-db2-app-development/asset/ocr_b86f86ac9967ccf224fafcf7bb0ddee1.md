```
Statement stmt=con.createStatement();
stmt.executeUpdate("delete from product where pid='101'");
SQLWarning sqlwarn=stmt.getWarnings();
while(sqlwarn!=null)
{
System.out.println("Warning description: " + sqlwarn.getMessage());
System.out.println("SQLSTATE: " + sqlwarn.getSQLState());
System.out.println("Error code: " + sqlwarn.getErrorCode());
sqlwarn=sqlwarn.getNextWarning();
}
Listing 4.16 - Handling a SQLWarning
```

# 4.3.5 Closing the connection

We include this section for completeness of the steps to develop a JDBC program. However, we have already shown in earlier examples how to close a connection using the **close** method of a connection. Earlier in Listing 4.4, we also illustrated how to close **Statement** and **ResultSet** objects, also using their corresponding **close** methods.

# 4.3.6 Working with XML

Working with pureXML in Java applications is fairly easy. Simply work with SQL/XML and XQuery statements the way you normally work with SQL statements. Treat XML as a string within the Java program. There are performance advantages as well. The JDBC program does not need to retrieve the entire XML document as a string or CLOB (if that was the way it was stored) and build at run time a DOM tree (if using DOM parser). The tree was already built when the XML document was inserted into the database. Let DB2 software ("DB2") retrieve what you need based on the SQL/XML or XQuery you passed to it.

# 4.3.6.1 Inserting XML data

If you want to insert a XML document to the database using a Java program, you have two choices:

+   - Hardcode the XML in the Java program and insert it as a string
+   - Store the XML document in a file, and insert the file using the **setBinaryStream** method

For example, let's assume you have created a table called CLIENTS with the following DDL:

```
create table clients(
    id        int primary key not null,
    name      varchar(50),
    status    varchar(10),
    contactinfo xml
```