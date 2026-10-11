By default, the InnoDB storage engine blocks new data inserts to the tables when it runs out of allocated storage space. You would have to manually extend the storage file size.

When you specify the autοexteηd setting, that allows the InnoDB storage engine to automatically allocate more space for the file. While that’s convenient, it can also be dangerous in some environments. The InnoDB storage engine keeps allocating more storage space as needed until the server runs out of disk space!

> When you use the InnoDB storage engine for your MySQL applications, it’s always a good idea to keep an eye on the storage space folder to make sure it’s not taking up all server disk space.

# Step 7: Customize the PHP Server

The PHP server configuration file is named php.ini, but can be located in several different areas. The locations that the PHP server checks are (in order):

+   1. The path set in the PHPIniDir directive in the Apache web server configuration file
+   2. The path set in a system environment variable named PHPRC
+   3. The folder where the PHP server executable file is stored
+   4. The default web server’s folder
+   5. The OS system folder, which for Linux is the /usr/local/lib folder

If you’re ever in doubt as to which php.ini configuration file the PHP server is using, run the phpinfo( ) function in a small PHP program, like this:

```
```PHP
<?php
phpinfo();
?>
```
```

Figure 21–2 shows the output from the phpinfo( ) function running on an Ubuntu system.

The phpinfo( ) function displays the system values for each of the configuration file settings, and if any were overridden by a local setting. Look for the Loaded Configuration File entry that shows the path to the active php.ini file to see where that file is located for your PHP server.