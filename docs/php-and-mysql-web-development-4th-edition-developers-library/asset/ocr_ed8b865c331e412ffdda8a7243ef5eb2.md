*mysql_install_db* populates the grant tables with initial accounts for the *root* and anonymous users. See Chapter 12, "General MySQL Administration," for details on these accounts and how to secure your installation by establishing passwords.

*mysql_install_db* is unavailable on Windows, but unnecessary because Windows distributions include a preinitialized data directory.

# F.8.1 Standard Options Supported by mysql_install_db

```
--help --user
```

--*help* is available as of MySQL 5.0,4/5.1,21.

On Unix, the --*user* option runs the server using the login account of the named user. This is useful for making sure that any directories and files created by the server are owned by this user if you run *mysql_install_db* as the Unix *root* user.

# F.8.2 Options Specific to mysql_install_db

You can use the options mentioned in this section on the command line, and you can set the values for many of them by placing appropriate entries in the [my*sql*ld] group of an option file. The script also reads the [my*sql*install_db] option group, which is useful for options such as --*l*data* and --*force* that are understood only by *mysql_install_db* and not by *my*sql*ld*.

*mysql_install_db* passes any unrecognized options to *my*sql*ld*.

+   - --*base*dir=dir_name
+   
+     The pathname to the MySQL base directory.
+   - --*data*dir=dir_name, --*l*data=dir_name
+   
+     The pathname to the MySQL data directory.
+   - --*force*
+   
+     Runs even if the current hostname cannot be determined. The IP number of the host will be used to create grant table entries instead, which means that to use client programs, you'll need to specify the IP number rather than the hostname except for connections to *localhost*.
+   - --*skip-name-resolve*
+   
+     Uses only IP numbers in the grant tables rather than hostnames. This option might be necessary if you don't have a working DNS server.

# F.9 mysqladmin

The *mysqladmin* client communicates with the MySQL server to perform a variety of administrative operations. You can use *mysqladmin* to obtain information from or control the operation of the server, set passwords, and create or drop databases:

```
mysqladmin [options] command ...
```