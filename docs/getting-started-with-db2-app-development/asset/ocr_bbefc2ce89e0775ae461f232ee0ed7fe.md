In the case of DB2, its JDBC and SQLJ driver is included in either of the following:

+   * Any DB2 data server edition

+   * IBM Data Server Client

+   * IBM Data Server Runtime Client

+   * IBM Data Server Driver for JDBC and SQLJ

Data server editions, clients and drivers were described in *Chapter 1 - What is DB2 Express-C?* Clients and drivers are free of charge. Depending on the type of JDBC driver you use in your application, you may require a client to be installed or not. The different types of JDBC drivers are explained in the next section.

# ## 4.2 Setting up the environment

Before you can run or develop JDBC or SQLJ applications ensure your environment is correctly set up.

If you would like to develop Java stored procedures and Java user-defined functions which reside on the DB2 server, ensure a JDK is installed in the DB2 server. Fortunately, when you install DB2 Version 9.7, the IBM SDK for Java 6 (also known as JDK 6) is installed by default on all platforms. The location where it is installed is indicated in the database manager configuration (**dbm cfg**) parameter **JDK_PATH**. For example, on Windows the default location is `C:\Program Files\IBM\SQLLIB\java\jdk`. The Java compiler (**javac**) at this location will be used to compile Java stored procedures and Java user-defined functions. The **JVM** that is part of this JDK is used to start the DB2 GUI tools such as the Control Center.

If you would like to develop JDBC/SQLJ applications from the DB2 server; in addition to the JDK, ensure the JDBC/SQLJ driver is setup correctly by adding the correct jar files to the **CLASSPATH**. Similarly, if you would like to develop JDBC/SQLJ application from a client machine, ensure you have installed and setup the JDBC/SQLJ driver correctly. If you are using the JDBC type 2 driver, you also need to install a DB2 client (either the IBM Data Server Client or the IBM Data Server Runtime Client). More details are provided in the next section.

# ### 4.2.1 DB2 JDBC and SQLJ drivers

*Table 4.1* describes the different types of JDBC drivers available in the industry today.

| Type | Driver name | Description | Provided with DB2? |
| :--- | :--- | :--- | :--- |
| Type 1 | The JDBC-ODBC bridge driver | Through this driver, JDBC access is performed via an ODBC driver. | No |