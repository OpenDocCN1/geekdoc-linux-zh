myprg3_SJProfile1.ser. These files hold information about the embedded SQL. From these files a myprg3_SJProfileKeys.class file (not shown in the figure) is created after `javac` is invoked. Using the DB2 customizer with the `db2sqljcustomize` command, a package (compiled SQL) is created in the database.

When you want to execute the program, simply run it using the command `java myprg3` which will use the myprg3.class file and the corresponding package in the database.

> Note:
> 
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

+   - `-url jdbc:db2://localhost:50000/sample` is the URL needed to connect to the database
+   - `-user rfchong` is user ID to connect to the database
+   - `-password mypasswd` is the password to connect to the database
+   - `myprg3_SJProfile0.ser` is the file name to customize to create the package in the database

The output would look as shown in *Listing 4.26* below.