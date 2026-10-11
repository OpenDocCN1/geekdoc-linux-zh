# 24.3 Targeting the Database

Web applications frequently have a database configured on another server as is the case in sandbox local. However, at this point we have network access to the database host and, for the most part, we can treat it as if we are on the same network. As is always the case with tunnels, we should expect some lag.

# 24.3.1   Enumeration

At this point in the enumeration step of the database, we already know a couple of things. Because of access to the WordPress server, we know that the host is in a different network than we are currently to. We also know that we are running MariaDB version 10.3.20. A quick Google search shows us this is a fairly new version. This presents a problem as a new version most likely won't have vulnerabilities that lead to remote code execution.

Let's connect to the database and start enumerating other aspects of MariaDB.

# 24.3.1.1 Application/Service Enumeration

To connect to MariaDB, we can use Kali's built in MySQL client along with the credentials we have recovered from the WordPress configuration file. While MariaDB is a different package than MySQL, it was designed to be backwards compatible. ${ }^{730}$ We will also need to point the MySQL client to the tunnel running on Kali on port 13306.

```
kali@kali:~$  mysql  --host=127.0.0.1  --port=13306  --user=wp  -p

Enter  password:

Type  'help;'  or  '\h'  for  help.  Type  '\c'  to  clear  the  current  input  statement.

MariaDB  [(none)]>
```

Listing 901 - Connecting to MariaDB

Now that we are connected, we can look at what privileges we have as the wp user and get a better idea of how this MariaDB instance is configured.

```
MariaDB  [(none)]>  SHOW  Grants;
+-------------------------------------------------------------
|  Grants  for  wp@%    |  
+--------------------------------------------------------------
|  GRANT  USAGE  ON  *.*  TO  'wp'@'%'  IDENTIFIED  BY  PASSWORD
  '*61163AE4B131AB0E43F07BE7B'   |
|  GRANT  SELECT,  INSERT,  UPDATE,  DELETE  ON  'wordpress' . *
  TO  'wp'@'%'    |  
+--------------------------------------------------------------
2  rows  in  set  (0.075  sec)
```

Listing 902 - wp user grants

We don't have \"*\" permissions, but SELECT, INSERT, UPDATE, and DELETE are a good starting point. Next, let's take a look at some variables and see if we can find anything that stands out.

```
MariaDB  [(none)]>  show  variables;
+------------------------------------------------------------+
|  variable_name  |  value   |  
+------------------------------------------------------------+
```

${ }^{730}$ (MariaDB, 2020). https://mariadb.com/kb/en/library/mariadb-vs-mysql-compatibility/