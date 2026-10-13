# PHP FAILS TO CONNECT TO MY DATABASE SERVER

Assuming you are using the correct username and password for your server, this problem is most likely to occur when the PHP server and the database server are on different machines on the network. If your database server restricts based on the host of origin of the connection, be sure to add the PHP server to the list of valid clients on the database server. Otherwise, connections will be refused.

Also, ensure that the host table (/etc/hosts) on the PHP server has an entry for the database server and that the host table on the database server has an entry for the PHP server.

Another problem when accessing a database with PHP is that your PHP installation may not have the appropriate library compiled into for the database server you are trying to access. In this case, you should recompile PHP as outlined earlier in the “Installing PHP” section.