# # SHELL COMMANDS

+   1.  **avail**
+       Print the **avail** list.
+   2.  **bucket** *NUM*
+       Print the bucket number *NUM* and set is as the current one.
+   3.  **cache**
+       Print the bucket cache.
+   4.  **close**
+       Close the currently open database.
+   5.  **count**
+       Print the number of entries in the database.
+   6.  **current**
+       Print the current bucket.
+   7.  **delete** *KEY*
+       Delete record with the given *KEY*.
+   8.  **dir**
+       Print hash directory.
+   9.  **export, e** *FILE-NAME* **[** *truncate* **]** **[** *binary* **|** *ascii* **]**
+       Export the database to the flat file *FILE-NAME*. This is equivalent to (1).
+       This command will not overwrite an existing file, unless the **truncate** parameter is also given. Another optional parameter determines the type of the dump (\*note Flat files::). By default, ASCII dump will be created.
+   10. **fetch** *KEY*
+       Fetch and display the record with the given *KEY*.
+   11. **first**
+       Fetch and display the first record in the database. Subsequent records can be fetched using the **next** command (see below).
+   12. **hash** *KEY*
+       Compute and display the hash value for the given *KEY*.
+   13. **header**
+       Print file header.
+   14. **help or ?
+       Print a concise command summary, showing each command letter and verb with its parameters and a short description of what it does. Optional arguments are enclosed in square brackets.
+   15. **import** *FILE-NAME* **[** *replace* **]** **[** *nometa* **]**
+       Import data from a flat dump file *FILE-NAME*. If the **replace** argument is given, any records with the same keys as the already existing ones will replace them. The **nometa** argument turns off restoring meta-information from the dump file.
+   16. **list**
+       List the contents of the database.
+   17. **next** [*KEY*]