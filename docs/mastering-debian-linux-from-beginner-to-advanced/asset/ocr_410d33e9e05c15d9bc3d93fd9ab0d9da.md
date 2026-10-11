+   8. Test PHP installation by creating a test file:

```
echo "<?php phpinfo(); ?>" | sudo tee
/var/www/html/phpinfo.php
```

+   9. Access the test file in your web browser:
+    http://your_server_ip/phpinfo.php

# **Database Management
(MySQL/MariaDB/PostgreSQL)**

Databases are essential for storing and managing data in many applications.
Let's explore how to work with popular database systems on Debian.

# **MySQL/MariaDB**

MySQL and MariaDB are popular relational database management systems.
MariaDB is a fork of MySQL and is often used as a drop-in replacement.

# **Basic MySQL/MariaDB Management**

+   1. Connect to MySQL/MariaDB:

```
sudo mysql
```

+   2. Create a new database: