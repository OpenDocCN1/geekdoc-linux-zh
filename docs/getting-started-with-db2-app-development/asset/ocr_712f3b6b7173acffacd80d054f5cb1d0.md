+   - #sql [connection-context, execution context] { sql statement }
+   - #sql { sql statement }
+   - #sql [execution context] { sql statement }

Host variables can be identified by a colon as in the example below:

```
```
#sql {SELECT EMPNO FROM EMP WHERE WORKDEPT = :dept};
```
```

# 4.4.2 Connection contexts

To work with SQL in an SQLJ program, you need to first establish a database connection. A connection context is used for that purpose. There are different ways to work with connection contexts as shown in *Listing 4.17* and *Listing 4.18* below.

+   (1) #sql context ctx; // This should be outside the class
+   (2) Class.forName("com.ibm.db2.jcc.DB2Driver").newInstance();
+   (3) ctx ctx1 = new ctx("jdbc:db2:sample", false);
+   (4) #sql [ctx1] { DELETE FROM dept };

# Listing 4.17 - Working with a Connection context

In the above listing:

+   (1) Declare a class for the connection context using the syntax:

```
```
#sql context <context-class-name>
```
```

+   (2) Load the JDBC driver; similar to JDBC programs.
+   (3) Invoke the constructor of the *context* class.
+   (4) An SQL statement (**DELETE**) is executed under the connection context **"ctx1"**.

This other example in *Listing 4.18* is similar but it combines using JDBC connection objects with SQLJ.

```
```
#sql context ctx; // This should be outside the class
Class.forName("com.ibm.db2.jcc.DB2Driver").newInstance();
(1) Connection con=DriverManager.getConnection();
(2) ctx ctx1 = new ctx(con);
#sql [ctx1] { DELETE FROM dept };
```
```

# Listing 4.18 - Connection context from Connection object example:

In the above listing:

+   (1) Using a **Connection** object
+   (2) Invoke the constructor of the *context* class.