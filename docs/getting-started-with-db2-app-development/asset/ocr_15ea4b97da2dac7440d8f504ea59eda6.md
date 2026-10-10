In this example, the names for the columns (\*lastname*, \*salary*) and table (\*employee*) referenced in a statement are fully known at precompile time. The following example is also a static SQL statement:

```
SELECT \*lastname*, \*salary\* FROM \*employee\* WHERE \*firstnm\* = :fname
```

In this second example, a host variable \*:fname* is used as part of an embedded SQL statement. Though the value of the host variable is unknown until runtime, its data type is known from the program, and all the other objects (column names, table names) are fully known ahead of time. DB2 software uses estimates for these host variables to calculate the access plan ahead of time; therefore, this case is still considered static SQL.

You precompile, bind, and compile statically executed SQL statements before you run your application. Static SQL is best used on databases whose statistics do not change a great deal. Now let’s take a look at one more example:

```
SELECT \*?, \*?\* FROM \*?\*
```

In this example, the names for the columns and table referenced by the statement are not known until runtime. Therefore the access plan is calculated only at runtime and using the statistics available at the time. These types of statements are considered \*Dynamic\* SQL statements.

Some programming APIs, like JDBC and ODBC, always use dynamic SQL regardless of whether the SQL statement includes known objects or not. For example, the statement \*SELECT\* \*lastname*, \*salary\* FROM \*employee\* has all the columns and table names known ahead of time, but through JDBC or ODBC, you do not precompile the statements. All the access plans for the statements are calculated at runtime.

In general, two statements are used to treat a SQL statement as dynamic:

+   • **\*PREPARE\***: This statement prepares or compiles the SQL statement calculating the access plan to use to retrieve the data
+   • **\*EXECUTE\***: This statement executes the SQL

Alternatively you can execute a **\*PREPARE\*** and **\*EXECUTE\*** in one single statement: **\*EXECUTE IMMEDIATELY\***

\*Listing 1.1\* shows an example on an embedded C dynamic SQL statement that is prepared and executed.

```
strcpy (hvStmtDyn, "SELECT \*name\* FROM emp WHERE dept = \*?\*" );
PREPARE Stm tDyn FROM :hvStmtDyn;
EXECUTE StmtDyn USING 1;
EXECUTE StmtDyn USING 2;
```

\*Listing 1.1\* - An embedded C dynamic SQL statement using **\*PREPARE\*** and **\*EXECUTE\***

\*Listing 1.2\* shows the same example as \*Listing 1.1\*, but using the **\*EXECUTE IMMEDIATELY\*** statement