```
```
-rw-r--r---   1 www-data www-data 2.9K Jan  7  2019 wp-config-sample.php
-rw-r--r---   1 www-data www-data 2.7K Dec  6 18:07 wp-config.php
drwxrwsr-x   6 www-data www-data 4.0K Dec  9 19:04 wp-content
...
```
```

```
```
 cat  wp-config.php
 
...
/** ** MySQL settings - You can get this info from your web host ** */
/** The name of the database for WordPress */
define( 'DB_NAME', 'wordpress' );

/** MySQL database username */
define( 'DB_USER', 'wp' );

/** MySQL database password */
define( 'DB_PASSWORD', 'Lv9EVQq86cfi8ioIwsqFUQyU' );

/** MySQL hostname */
define( 'DB_HOST', '10.5.5.11' );
... 
```
```

*Listing 890 - Reading wp_config.php*

In the **wp_config.php** file, we find that the database IP address is set to 10.5.5.11. We also discovered a MariaDB username of “wp” and that the password for this account is "Lv9EVQq86cfi8ioIwsqFUQyU". To continue, we need to solidify our foothold into the network and create a stable pivot point.

# 24.2.7       Creating a Stable Pivot Point

Before continuing, let’s review what we currently have. We have a shell on the WordPress box as the www-data user and we also have network access to the database via Ajax. Finally, we just discovered database credentials that we know are valid since they are already in use by the WordPress application.

So far, we know that the network should look something like Figure 340.

![](bbox=[0.15, 0.65, 0.85, 0.76])

*Figure 340: Network Diagram with Database Hostname Unknown*

Since the WordPress machine and the database box are on separate networks, this is a great time to use a tunnel. However, our choices are limited due to fact that our reverse shell is running in the context of an unprivileged user account without a valid login shell (www-data).

Since ssh (the client) is a core application that is included in almost every Linux distribution, we can attempt to use it to create a reverse tunnel. One caveat is that since we do not have root access to create a login for the www-data user, we will need to use the SSH client on the WordPress machine to log in to our Kali server to create the tunnels. In short, we’ll need a reverse tunnel.