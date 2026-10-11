Under Unix, relocate a database as follows:

+   1. Stop the server if it is running.
+   2. Move the database directory to its new location, or copy it and remove the original.
+   3. Create a symlink in the data directory that has the name of the original database and that points to the new database location.
+   4. Restart the server.

The following example shows how to relocate a database bigdb from the `/usr/local/mysql/data` directory to `/var/db`:

```
% mysqldadmin -p -u root shutdown
Enter password: ******
% cd /usr/local/mysql/data
% tar cf - bigdb | (cd /var/db; tar xf -)
% rm -rf bigdb
% ln -s /var/db/bigdb bigdb
% mysqld_safe &
```

You should execute these commands while logged in as the MySQL administrator. Under Windows, database relocation is handled somewhat differently:

+   1. Stop the server if it is running.
+   2. Move the database directory to its new location, or copy it and remove the original.
+   3. Create a file in the MySQL data directory that acts as a symbolic link to let the MySQL server know where to find the relocated database directory. The file should have a `.sym` extension and a basename that is the database name. For example, if you move the sampdb database from C:\\mysql\\data\\sampdb to E:\\mysql\\-book\\sampdb, you should create a file named `C:\\mysql\\data\\sampdb.sym` that contains this line:
+       E:\\mysql\\-book\\sampdb\\
+   4. Make sure that symbolic link support is enabled when you restart the server. Windows servers should have this enabled by default, but you can enable it explicitly by using the `--symbolic-links` option on the command line or by placing these lines in an option file:
+      `[mysqld]`
+      `symbolic-links`

If you're moving a database to another filesystem as an attempt to redistribute database storage, remember that if you are using InnoDB tables that are stored in the InnoDB shared tablespace, the contents of those tables are not located in the database directory. For a database composed primarily of such InnoDB tables, relocating the database directory