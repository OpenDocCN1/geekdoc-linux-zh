
### 4.2.4 Iterators

(9)
    #sql { fetch :iterator1 into :poid, :status }
    );

#### Listing 4.23 - An example of a position iterator

In the above listing:

1. A position iterator is declared with two columns. Note that the column does not have names, just the data type. This is why this is a position iterator
2. A variable `status` is declared. This is like a host variable that are used to receive the values from the iterator
3. Similar to (2) for variable `poid`.
4. A positioned iterator `iterator1` is created.
5. In connection context `ctx1`, the `iterator1` is defined with a `select poid, status from purchaseorder`
6. Before starting the loop, we fetch the first record into the host variables `poid` and `status`. This is because in (7) we are not using `next()`, but `endFetch()` so the while loop condition would end differently if you use `next()` vs. `endFetch()`.
7. Looping through the iterator
8. Printing the `poid` and `status` of each row retrieved.
9. Fetching the next record in the iterator.

Named or position iterators can be updatable and scrollable. By default, iterators in SQLJ are read-only and can only move forward. To define a scrollable iterator, you need to implement `sqlj.runtime.Scrollable` while defining the iterator.

To define an updatable cursor, you need to implement `sqlj.runtime.ForUpdate` while defining the iterator. When defining an updatable iterator, you also need to specify the columns you would like to update.

This is similar as in JDBC. Listing 4.24 provides an example of an updatable iterator.

(1)
    #sql public iterator namediterator implements sqlj.runtime.ForUpdate
    with (updateColumns="STATUS") (int poid, String status);
(2)
    namediterator iterator1;
(3)
    #sql {ctx1 { iterator1 = { select poid, status from purchaseorder };
(4)
    while (iterator1.next()) {
(5)
    System.out.println("before update poid: " + iterator1.poid() +
    " Status: " + iterator1.status());
(6)
    if (iterator1.status().toUpperCase().compareTo("UNSHIPPED") == 0) {
    #sql {ctx1 { update purchaseorder set status =
    'shipped' where current of : iterator1 };
    }
(7)
    #sql {ctx1 { commit; }

#### Listing 4.24 - An example of an updatable iterator

In the above listing:

1. A named iterator is declared and it's defined as updatable iterator because it implements `sqlj.runtime.ForUpdate` and note it also indicates which column it will be updating in `with (updateColumns="STATUS")`
2. The named iterator *iterator1* is declared
3. *iterator1* is defined as the result of the `select poid, status from purchaseorder`
4. Looping through the iterator
5. Printing each row of the iterator
6. Testing if the value of the *status* column is "UNSHIPPED". If it is, the value is changed to 'shipped'.
7. Committing the changes.

### 4.4.5 Working with JDBC and SQLJ combined

JDBC and SQLJ can be used together in a single application. For example, a JDBC connection object can be retrieved from a `ConnectionContext` object using its `getConnection` method and vice versa.

An iterator in SQLJ and a JDBC `ResultSet` can be retrieved from each other as shown below:

- Iterator from result set: `#sql iterator = {CAST :result-set }`
- Result set from an iterator: Use the iterator's `getResultSet` method.

*Listing 4.25* provides an example of working with JDBC and SQLJ combined in one program.

```java
#sql public iterator positionIterator (int, String);
Class.forName("com.ibm.db2.jcc.DB2Driver").newInstance();
Connection con=DriverManager.getConnection(url);
con.setAutoCommit(false);
(1) ctx ctx1=new ctx(con);
positionIterator iterator;
Statement stmt = con.createStatement();
ResultSet rs=stmt.executeQuery("select poid, status from purchaseorder");
(2) #sql [ctx1] iterator={cast :rs};
#sql {fetch :iterator into :poid, :status};
while(!iterator.endFetch()) {
System.out.println("id: "+poid+" status: "+status);
#sql {fetch :iterator into :poid, :status};
}
    iterator.close();
```

**Listing 4.25 - Working with JDBC and SQLJ combined in one program**

In the above listing:

1. The connection object is used to create an SQLJ connection context
2. This shows how an SQLJ iterator can be obtaining the results coming from a JDBC result set

### 4.4.6 Preparing an SQLJ program

Preparing an SQLJ program is similar to the process followed for an embedded SQL program where you have to precompile and bind the program. In this case, the SQLJ program needs to be translated and customized. *Figure 4.11* shows the process to prepare the program `myprg3.sqlj`.

![](img/5f6ba170efa3a607142589708531bef8_155_0.png)

**Figure 4.11 - Steps to prepare a SQLJ program**

In the figure, the SQLJ program `myprg3.sqlj` goes through the *SQLJ Translator* using the `sqlj` command. The SQLJ Translator inspects the file looking for lines starting with "#sql", and replaces those lines with generated code that includes the SQLJ runtime classes, creating a file with `.java` extension. It then compiles this file using the Java compiler (**javac**) to create a `.class` file. This is shown at the bottom of the figure where the `myprg3.java` and the `myprg3.class` files are created.

The SQLJ translator will also create, as shown at the top of the figure, serialized profile files for each connection context class that is used in an SQLJ executable clause. In this example it shows two serialized profile files `myprg3_SJProfile0.ser` and `myprg3_SJProfile1.ser`. These files hold information about the embedded SQL. From these files a myprg3_SJProfileKeys.class file (not shown in the figure) is created after `javac` is invoked. Using the DB2 customizer with the `db2sqljcustomize` command, a package (compiled SQL) is created in the database.

When you want to execute the program, simply run it using the command `java myprg3` which will use the myprg3.class file and the corresponding package in the database.

> **Note:**
> The program `myprg3.sqlj` is included in the zip file `Exercise_Files_DB2_Application_Development.zip` accompanying this book. You can review, test, and prepare this file.

Below is an example of actually executing all of these commands and the corresponding output. These are the steps to follow:

(1) Running the SQLJ Translator (`sqlj` command)

```
D:\>sqlj myprg3.sqlj
```

The following files are created:

```
myprg3.java, myprg3.class,
myprg3_SJProfile0.ser,
myprg3_SJProfileKeys.class
```

(2) Run the DB2 Customizer (`db2sqljcustomize` command) for every .ser file. The DB2 Customizer can take several parameters. It's basically a Java program that needs to connect to a database since that's where it will store the package. For example:

```
D:\>db2sqljcustomize -url jdbc:db2://localhost:50000/sample -user rfchong -password mypasswd myprg3_SJProfile0.ser
```

Where:

- `-url jdbc:db2://localhost:50000/sample` is the URL needed to connect to the database
- `-user rfchong` is user ID to connect to the database
- `-password mypasswd` is the password to connect to the database
- `myprg3_SJProfile0.ser` is the file name to customize to create the package in the database

The output would look as shown in *Listing 4.26* below.

```
[jcc][sqlj]
[jcc][sqlj]  Begin Customization
[jcc][sqlj]  Loading profile: myprg3_SJProfile0
[jcc][sqlj]  Customization complete for profile myprg3_SJProfile0.ser
[jcc][sqlj]  Begin Bind
[jcc][sqlj]  Loading profile: myprg3_SJProfile0
[jcc][sqlj]  Driver defaults(user may override):  BLOCKING ALL
VALIDATE BIND STATIC READ_ONLY YES
[jcc][sqlj]  Fixed driver options: DATETIME ISO DYNAMICRULES BIND
[jcc][sqlj]  Binding package MYPRG301 at isolation level UR
[jcc][sqlj]  Binding package MYPRG302 at isolation level CS
[jcc][sqlj]  Binding package MYPRG303 at isolation level RS
[jcc][sqlj]  Binding package MYPRG304 at isolation level RR
[jcc][sqlj]  Bind complete for myprg3_SJProfile0
```

**Listing 4.26 - Output of running the DB2 customizer**

No output files will be created, but a package with the embedded SQL statements and access plan would be stored in the database.

(3) Run the program. The package previously created is then used at runtime.

```
D:\>java myprg3 <userid> <password>
Successful connection to the database!
Successful retrieval of record. Column 'IBMREQD' has a value of 'Y'
Successful Disconnection from database
End of Program
```

Figure 4.12 below shows all the output of preparing the program myprg3.sqlj.
