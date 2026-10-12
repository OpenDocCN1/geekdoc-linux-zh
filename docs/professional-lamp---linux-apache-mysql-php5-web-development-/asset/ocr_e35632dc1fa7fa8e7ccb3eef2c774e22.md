# Chapter 7

and a fair number of protected directories, it can quickly become a nightmare to ensure the proper users are in the proper groups, with access to the proper resources, with current passwords, and so on.

Simple authentication with Apache can also be a problem if you’re dealing with multiple load-balanced or mirrored web servers. Because the user credentials are stored on each machine, you can end up in a state of file disparity — some password files might contain a different number of users, with different passwords, or other problems.

As an alternative to simple file-based authentication with Apache, you can also use the mod_auth_mysql Apache module, also covered in Chapter 6. Using mod_auth_mysql centralizes your username/password storage, and also gives you the ability to do complex permission-matching abilities — not a simple user-name-match as with the standard Apache Basic Authentication.

Like simple authentication with Apache, mod_auth_mysql relies on access rights specified in .htaccess files or a <Directory> entry in httpd.conf. If you do not have access to change the Apache configuration, and .htaccess files aren’t permitted by your host, you’ll need to find another method. Enter PHP-based authentication.

# PHP-Controlled Authentication

If Apache-controlled authentication is out of the question, you can actually use the power of PHP to emulate standard Basic Authentication. By sending the proper response headers, and checking for the right server variables, you can build your own basic authentication system from scratch, and it’ll have just as much power as mod_auth_mysql, if not more.

To show how you can use PHP for basic authentication, you’re going to set up a simple database to use as your repository for user credentials. PHP will then check the usernames and passwords against that database; all the end-user will see is the standard Basic Authentication prompt.

# Creating the Authentication Database

Start by creating a database in MySQL called WebAuth

```
CREATE DATABASE WebAuth;
USE WebAuth;
```

Next, create a MySQL login for the authentication system, and give it read-only access to the database you just created:

```
GRANT SELECT ON WebAuth.* To WebAuth@localhost IDENTIFIED BY 'AuthPass';
```

Now, set up the table to hold the usernames and passwords. In this example, the table will store just the username and hashes of the password, but if you wanted, you could easily add extra fields for any other access criteria you want.

```
CREATE TABLE Users (username varchar(50) PRIMARY KEY,
    passwd_md5 varchar(32) NOT NULL,
    passwd_sha1 varchar(40) NOT NULL);
```