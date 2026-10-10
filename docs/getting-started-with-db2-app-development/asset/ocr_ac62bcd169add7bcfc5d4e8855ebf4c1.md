+   2. Prepare a **SELECT** SQL statement by calling the database handle’s **prepare** method, which returns a statement handle if the SQL is successfully prepared.
+   
+      For example, you can call the **prepare** method with an **SELECT** statement passed in as a string argument as follows:
+   

```
    $sthandle = $dbh->prepare(
       "SELECT firstname, lastname
           FROM employee WHERE workdept='A00'");

```

Where **$dbh** is the database handle returned from step 1 and **$dbh->prepare** returns a statement handle in the variable **$sthandle** if the statement is successfully prepared.


+   3. Execute the prepared **SELECT** statement by calling the **execute** method using the statement handle. After a successful execution of the SQL, the statement handle will be associated with the result set.
+   
+      For example, you can execute the statement prepared in the previous step by using the following Perl statement:
+   

```
    $rc = $sth->execute();

```

+   4. Fetch rows from the result set associated with the statement handle by calling **fetchrow_array()** method on the statement handle, which returns a row as an array with one value for each column.
+   
+      For example, you can fetch the rows from the above statement handle **$sth** as shown in Listing 9.7.
+   

```
    while (($fname, $lname) = $sth->fetchrow_array()) {
       print "$fname $lname\n";
    }

```

**Listing 9.7 – Fetch rows from the result set**


> **Note:** In addition to `fetchrow_array`, the statement handle also provides many other data fetching methods, such as `fetchrow_arrayref`, `fetchrow_hashref`, `fetchall_arrayref`, `fetchall_hashref`, to support flexible ways of fetching rows from a result set. For more information about these functions, refer to [http://search.cpan.org/~timb/DBI/DBI.pm](http://search.cpan.org/~timb/DBI/DBI.pm).
> 

The above code snippets are part of the script **select.pl** included in the **Exercise_Files_DB2_Application_Development.zip** file accompanying the book.