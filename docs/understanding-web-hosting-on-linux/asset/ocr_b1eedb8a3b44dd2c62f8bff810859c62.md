The Java designers at Sun Microsystems looked at ODBC and decided, rather providing a Java API to ODBC, to improve and simplify ODBC. The result is JDBC, or Java Database Connectivity. The designers at Sun did a great job. JDBC is powerful, yet easy to learn and use.

The JDBC API was based on ODBC, although its developers simplified the interface and streamlined processing. Initially, the only JDBC drivers used ODBC drivers in the background to connect with your RDB choice. You used the default JDBC driver that was (and still is) shipped with the Java Development Kit (JDK). That driver is known as a JDBC-to-ODBC driver because it requires an ODBC driver.

The problem with JDBC-to-ODBC drivers is that your applications run slowly because you are essentially using two middleware products. RDB vendors saw the potential for Java, however, and developed "100% pure" JDBC drivers that did not require the use of ODBC drivers. Many of these JDBC drivers were faster than their ODBC counterparts, and most RDB vendors made their JDBC drivers available for free. Eventually, for optimal performance, RDB vendors created what are known as native JDBC drivers. These drivers were implemented to use the architecture of the RDB's native platform, rather than the interpreted cross-platform Java language. The iSeries, for instance, has a 100% pure JDBC driver for cross-platform client access to DB2/400, and a native JDBC driver for host-based access to DB2/400. The AS/400 Toolbox for Java (www.iseries.ibm.com/toolbox/downloads.htm) contains the pure JDBC driver. The AS/400 Developer Kit for Java (AS/400 license license program 5769-JV1) contains the native AS/400 JDBC driver.

# The JDBC API

JDBC has four components:

+   - Driver manager
- Host connection
- SQL statement
- Result set

Components in Java are classes. (Remember that, as yet, discussion has not turned to IBM's Java Toolbox for the AS/400.) These four components, and the associated JDBC utility classes, are standard JDBC classes and—in theory—conform to the JDBC standard published by Sun. However, your JDBC Java code could access DB2/400 one day, and the next day, after one of those nasty mergers, access Oracle or been.

The following JDBC classes encapsulate the features of the corresponding JDBC components:

+   - DriverManager
- Connection
- Statement
- ResultSet

The DriverManager class tells the Java Virtual Machine (JVM) which driver you are using. The specifies the AS/400 Toolbox for Java's 100% pure JDBC driver:

```
Class.forName("com.ibm.as400.AS400JDBCDriver");
```