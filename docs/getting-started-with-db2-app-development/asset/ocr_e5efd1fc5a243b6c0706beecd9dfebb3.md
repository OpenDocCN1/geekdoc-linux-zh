```
(3) print "First Name: %s, Last Name: %s" % (mytuple[0], mytuple[1])
(4) mytuple = ibm_db.fetch_tuple (stmt)
```

# Listing 10.6 – Fetch rows from the result set

Items in *Listing 10.6* are explained as follows:

+   (1) The function **ibm_db.fetch_tuple** returns each row from the result set as a tuple and assigns it to the variable *mytuple*;
+   (2) Loop until the function returns **False** if there are no rows left in the result set;
+   (3) Print each columns' value from the returned row by using the 0-indexed column position, such as *mytuple[0], mytuple[1]*;
+   (4) Fetch the next row into the variable *mytuple*.

> **Note:**
> 
> In addition to **ibm_db.fetch_tuple**, the ibm_db driver also provides 3 other data fetching functions that support flexible ways of fetching result sets: **ibm_db.fetch_assoc**, **ibm_db.fetch_both** and **ibm_db.fetch_row**. For more information review [http://code.google.com/p/ibm-db/wiki/APIs](http://code.google.com/p/ibm-db/wiki/APIs).

If you would like to test all the above code snippets, edit the Python script `select.py` included in the exercise files accompanying this book and replace the user ID and password with your own. Then run the script as follows:

```
`python select.py`
```

The result of executing the above script is illustrated in *Figure 10.5*.

![](bbox=[0.14, 0.6, 0.84, 0.7])

Figure 10.5 Executing the script select.py

> **Note:**
> 
> All the scripts used in this chapter are included in the directory *samples/chapter10* in the zip file *Exercise_Files_DB2_Application_Development.zip* that accompanies this book.
> To run the scripts, you may need to first create the *SAMPLE* database using the *db2samp1* utility. Also replace the user name and password in the scripts with your own ones.