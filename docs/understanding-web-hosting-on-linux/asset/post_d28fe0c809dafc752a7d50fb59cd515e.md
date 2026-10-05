
do you want the comments to be shown in the generated HTML, use the standard HTML comment tags of (<!-- and -->).

# End of Chapter Review

## Key Terms

| Arrays | Get/Post | Strings |
| --- | --- | --- |
| Comments | JavaServer Pages | Tomcat |
| Conditional statements | Object-oriented language | Unary operators |
| Constants | Operators | Variables |
| Data types | Scriptlets | WebSphere |
| Declaration statements | Servlets | |

## Review Questions

- 1. What are the advantages of using Java?
- 2. Explain Just-in-Time (JiT) compilation.
- 3. What are the three types of Java programs?
- 4. Where do servlets run?
- 5. What are JavaServer Pages?

# Programming Assignment

## Exercise 1: Code and Test Your First Java Application

- 1. Download the Sun JDK from http://java.sun.com and install it using directions in the chapter.
    - a) Be sure to modify your path to contain the qualification of the JDK's bin directory.
    - b) Be sure to set the JAVA_HOME environment variable to point to the JDK directory.
    - c) Test for proper JDK installation:

```
$ java -version
```

- 2. Enter the code in Figure 7.4 into a file called Test.java.
    - a) Use the javac command to compile it:
    - b) Once any potential errors are corrected, use the java command to test the application:

```
$ javac Test.java
```

```
$ java Test
```

## Exercise 2: Install a Web Application Server

- 1. Following the directions in the chapter, install Tomcat

- 2. Start Tomcat:

```
$ cd /jakarta-tomcat/bin
$ sh startup.sh
```

- 3. From Netscape Navigator, request Tomcat's home page using the following URL:

```
http://127.0.0.1:8080
```

- 4. Walk through all of the links on Tomcat's home page to view the various technologies supported by server-side Java.

## Exercise 3: Create Your First Java Servlet

- 1. Copy the Panel.html file created in exercise 2 of chapter 6 to the tom/webapp/ROOT directory.

- 2. Access Panel.html from Netscape Navigator served by Tomcat, using the following URL:

```
http://127.0.0.1:8080/Panel.html
```

- 3. Fill in the form, and click the Submit button. An error will be presented saying that the PanelServlet was not found or available. To fix that error, you'll have to deploy PanelServlet.

- 4. Using your favorite Linux editor, create a file called PanelServlet.java and enter the Java source shown in Figure 7.8.

- 5. To compile the source, you'll have to set the CLASSP environment variable to point to the Java archive that contains the Servlet API Java classes:

```
$ CLASSPATH=CLASSPATH:/opt/tomcat/lib/servlet.jar
```

- 6. Use the javac command to compile PanelServlet.java:

```
$ javac PanelServlet.java
```

- 7. Once any errors are corrected and the compile completes successfully, copy the Java executable, PanelServlet.class, to /opt/tomcat/webapps/ROOT/WEB-INF/classes:

```
$ PanelServlet.class /opt/tomcat/webapps/ROOT/WEB-INF/classes
```

- 8. Access Panel.html from Netscape Navigator served by Tomcat.
    - a) Fill out the form and click Submit.

Notice that PanelServlet simply echoes the values keyed. A production servlet would do some more complex processing and relational database access.

## Exercise 3: Create Your First JavaServer Page

- 1. Copy Panel.html to a new file in the same directory. Call it Panel.jsp.

- 2. List the contents of tomcat/work/localhost_8080.

- 3. Access Panel.jsp, which should look exactly like Panel.html:

```
http://127.0.0.1:8080/Panel.jsp
```

- 4. List the contents of tomcat/work/localhost_8080 and take note of the new Java source file created by Tomcat's JSP compile process. (It will have Panel in its name.)

- 5. Use the less command to look at the Java source file. Look for the HTML tags from Panel.jsp.

- 6. Using your favorite Linux editor, edit Panel.jsp to add a JSP expression that outputs today's date:

```
Today's date <%=(new java.util.Date()).toLocaleString() %>
```

- 7. Access Panel.jsp again:

```
http://127.0.0.1:8080/Panel.jsp
```

- 8. List the contents of the new Java source file in Tomcat's work/localhost_8080 directory and find the date code that you added to the JSP.

# 8

# RDB, SQL, and JDBC

Relational databases (RDBs) are the predominant storage mechanism for business information. In this chapter, you learn what an RDB is, how to create and maintain an RDB using Structured Query Language (SQL) commands, and how to automate SQL in Java applications with Java Database Connectivity (JDBC).

You are probably already comfortable with the concept of a database, but you might be unfamiliar with the concept of a relational database. Basically, a relational database is a set of tables. Each table in the database contains rows and columns. The rows in a table represent individual records, while the columns represent the attributes of those records.

Relational databases (RDBs) are the predominant storage mechanism for business information. In this chapter, you learn what an RDB is, how to create and maintain an RDB using Structured Query Language (SQL) commands, and how to automate SQL in Java applications with Java Database Connectivity (JDBC).

You are probably already comfortable with the concept of a database, but you might be unfamiliar with the concept of a relational database. Basically, a relational database is a set of tables. Each table in the database contains rows and columns. The rows in a table represent individual records, while the columns represent the attributes of those records.

Relational databases (RDBs) are the predominant storage mechanism for business information. In this chapter, you learn what an RDB is, how to create and maintain an RDB using Structured Query Language (SQL) commands, and how to automate SQL in Java applications with Java Database Connectivity (JDBC).

You are probably already comfortable with the concept of a database, but you might be unfamiliar with the concept of a relational database. Basically, a relational database is a set of tables. Each table in the database contains rows and columns. The rows in a table represent individual records, while the columns represent the attributes of those records.

Relational databases (RDBs) are the predominant storage mechanism for business information. In this chapter, you learn what an RDB is, how to create and maintain an RDB using Structured Query Language (SQL) commands, and how to automate SQL in Java applications with Java Database Connectivity (JDBC).

# Table 8.1: A Simple Accounts-Receivable Database

| Invoice | CustNo | LastName | State | LineNo | Desc | Qty | InvoiceDate |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1234 | 981 | Denoncourt | CA | 1 | Bolts | 2 | 11/10/1999 |
| 1234 | 981 | Denoncourt | CA | 2 | Washers | 15 | 11/10/1999 |

A major benefit of RDBS is that you control redundant information. The information related to a customer is stored in one row. The information about an invoice is stored in another row. If relating to one business entity were duplicated in the rows of various tables, the integrity of information would be difficult to maintain.

# Table 8.2: A Virtual Formed By Joining Files Using Their Key Relationships

| Invoice | CustNo | LastName | State | LineNo | Desc | Qty | InvoiceDate |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 1234 | 981 | Denoncourt | CA | 1 | Bolts | 2 | 11/10/1999 |
| 1234 | 981 | Denoncourt | CA | 2 | Washers | 15 | 11/10/1999 |
