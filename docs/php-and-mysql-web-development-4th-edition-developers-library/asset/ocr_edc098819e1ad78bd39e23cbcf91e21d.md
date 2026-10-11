```
```
--with-mysqld=/usr/local/mysql/mysql_config
--with-mysql=/usr/local/mysql
--with-zlib
```
```

The options are used as follows. For each option that includes a pathname value, if `configure` can determine the location of the required information for itself, you can give the option without the pathname.

+   - `--with-apxs[=/path/to/apxs]`
+   
+     Tells `configure` where to find `apxs`, the Apache Extension Tool helper script that provides other modules with information about your Apache configuration.
+   
+   - `--enable-pdo`
+   
+     Includes support for the PDO extension.

+   - `--with-pdo-mysql[=/path/to/mysql]`
+   
+     Includes MySQL support for PDO. The pathname indicates where MySQL is installed so that `configure` can determine where the MySQL header files and libraries are located.

+   - `--with-mysqld[=/path/to/mysql_config]`
+   
+     Includes support for the `mysqld` "MySQL improved" extension. *This option is not needed for PDO*. You might use this option to enable people who aren't using PDO to run scripts based on the `mysql` extension. `/path/to/mysql_config` is the pathname to the `mysql_config` script. `configure` invokes the script to obtain MySQL configuration information.

+   - `--with-mysql[=/path/to/mysql]`
+   
+     Includes support for `mysql`, the original MySQL extension. *This option is not needed for PDO*. You might use this option to build in `mysql`, to enable people who aren't using PDO to run scripts based on the original extension. The pathname indicates where MySQL is installed so that `configure` can determine where the MySQL header files and libraries are located.

+   - `--with-zlib`
+   
+     This option is needed because the MySQL client library accesses compression functions.

After configuring PHP, build and install it as follows (you might need to be *root* to perform the installation commands):

```
```
$ make
# make install
# cp php.ini-dist /usr/local/lib/php.ini
```
```

The `cp` command installs a baseline PHP initialization file where PHP can find it. You can substitute `php.ini-recommended` for `php.ini-dist` if you like. Take a look at both and choose the one you prefer.