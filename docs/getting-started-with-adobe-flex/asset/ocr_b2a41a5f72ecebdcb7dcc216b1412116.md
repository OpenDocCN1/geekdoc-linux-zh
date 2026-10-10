![](bbox=[0.16, 0.15, 0.83, 0.41])

# Figure 7.7 - Architecture of a sample Flex application that accesses a DB2 database

As shown in the figure, the application flow is as follows:

+   1. The Flex application makes an HTTPSService call to the JSP residing on the Tomcat Server.
+   2. This JSP in turn makes a call to the Java class that contains the business logic to access the data from the database.
+   3. The Java class accesses the data from the database by sending the query for execution to the database.
+   4. The database returns a result set back to the invoker.
+   5. The Java class returns the data formatted as an *Employee* object or a list of *Employee* objects.
+   6. The JSP now formats the data received from the Java class as XML and sends it back to the Flex application.

> **Note:**
> This section assumes the reader has working knowledge of Java, JSP, and JDBC. For more information about these topics refer to the ebook *Getting started with Java* which is part of the DB2 on Campus book series.

The application uses the Flex front-end to perform the following tasks:
* Display the list of employees
* Display details of a particular employee selected.
When the application development is completed, it will look like in *Figure 7.8*.