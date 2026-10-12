
### DeflateFilterNote

If you wanted your log files to show the compression ratio for each requested file in the access log, use **DeflateFilterNote**. **DeflateFilterNote** takes the name of a log token as its value — the named token given with **DeflateFilterNote** can then be used to customize the output of your logs using Apache’s LogFormat directive.

### DeflateWindowSize

This specifies the zlib compression window size, used in compressing the files. Values range from 1 to 15, with 1 yielding less compression and 15 giving the most compression. The default value for **DeflateWindowSize** is 15.

## How Well Does mod_deflate Work?

In order to see the byte-saving abilities of mod_deflate, this example serves a decent-sized HTML page with Apache, both with and without mod_deflate enabled. In this example, the home page is used for the Wrox P2P community forums, found at `http://p2p.wrox.com`. The raw HTML markup — and the HTML only — for this page weighs in at a hefty 47172 bytes. Have a look at the following table to see how it fared being thrown through mod_deflate at three different compression levels:

| Compression Level | Bytes Transferred | % of Original | Approx. Download Time (56k) |
| :--- | :--- | :--- | :--- |
| Raw | 47172 bytes | 100% original | 11.7 seconds |
| Default (6) | 7621 bytes | 16.2% original | 3.8 seconds |
| Level 1 | 9050 bytes | 19.2% original | 4.1 seconds |
| Level 9 | 7581 bytes | 16.1% original | 3.8 seconds |

As you can see, using mod_deflate clearly has an advantage over serving the raw, uncompressed HTML — eliminating up to nearly 84% of the file size sent over the connection. Also notice that using the maximum compression of 9 edged out the default level of 6 by only a marginal amount, so in this situation it would probably be safe to stick with the default compression level of 6 to save the processor a few cycles.

Many websites have a mixture of HTML, media, and associated scripting files, so sites such as photo-blogs or online shopping malls may not reap tremendous file savings on every file they serve, but each byte saved can really add up to some huge bandwidth reduction at month’s end. Text-heavy sites such as blogs and news portals would really see the benefits of content compression, as a majority of the bandwidth utilized on those sites is plain text — text that would find its way through mod_deflate.

## Enabling Compression for PHP Scripts

What about PHP files you might be wondering? In many situations there is no need to use compression on PHP files, and in some cases it can be detrimental to the output.

If your PHP script outputs an actual image or PDF for example, you wouldn’t want Apache to blindly compress the output, just because the file extension happened to be .php.

In some situations, output buffering and compression might already be enabled for all PHP scripts. To determine, check the value of the configuration variable `output_handler`, or look in `php.ini` for the values of `output_handler` and `zlib.output_compression`.

To enable output compression within PHP, do the following:

1. Install the zlib libraries on your machine if needed.
2. Configure the PHP source code as needed, making sure you include `--with-zlib`, and then `compile/install` as normal.
3. Modify your `php.ini` so it includes the following lines:
   ```
   output_buffering = Off
   output_handler =
   zlib.output_compression = On
   ```
4. Restart Apache so the new changes take effect.

# Using MySQL with Apache

By now, you’ve created a security zone or two using Apache and basic authentication, and for most situations, that might be all you need. You may find, however, that basic authentication with Apache, while simple, is a little too limited in the amount of control and customization you can incorporate. For many such situations, you can actually use a combination of Apache basic authentication and the power of relational databases via MySQL. For such a purpose, the `mod_auth_mysql` Apache module exists.

Like standard Apache basic authentication, `mod_auth_mysql` can control access per-directory, and can be configured inside both `.htaccess` files and a `<Directory>` section inside `httpd.conf`. Unlike standard Apache basic authentication, all user credentials are stored in a database, instead of in flat files.

## Setting Up the Database

Installing and configuring `mod_auth_mysql` involves a few steps, the first of which is to create the necessary database structures to hold the user data. Start by loading up your favorite MySQL client, and creating the database. For example:

```sql
CREATE DATABASE apacheauth;
```

Next, create a user that will be used by Apache to access the credentials:

```sql
GRANT SELECT ON apacheauth.* TO apache@localhost IDENTIFIED BY ‘apachepass’;
```

Now that the database user is created, it’s time to add a table to hold the login information. For now start out with a simple table that just holds the username and password:

```sql
USE apacheauth;
CREATE TABLE user_info (
    user_name varchar(50) NOT NULL,
    user_password varchar(50) NOT NULL,
    PRIMARY KEY (user_name)
);
```

You can name the table and columns however you like. In the preceding example, **user_info** is used for the table name, and **user_name** and **user_password** are used for the login/password combination because these are the default names recognized by **mod_auth_mysql**.

> In later versions of mod_auth_mysql, the default column for password is **user_password**, not **user_passwd** as it states in the module documentation.

Next, create an initial test user account that you'll use later when testing the authentication:

```sql
INSERT INTO user_info (user_name, user_password)
VALUES ('testuser', SHA1('testpass'));
```

> Notice that the SHA1() function is used on the password in the statement, instead of the PASSWORD() function. With mod_auth_mysql you can use a handful of encryption methods for the password — this example just happens to use SHA1.

## Installing the Module

Once you have your database table set up, you'll need to actually download the source for **mod_auth_mysql**, available at [http://modauthmysql.sourceforge.net](http://modauthmysql.sourceforge.net). At the time of this writing, the current version was 2.9.0, so you would download **mod_auth_mysql-2.9.0.tar.gz**.

After you've downloaded the module source, extract the tarball:

```bash
tar -xzvf mod_auth_mysql-2.9.0.tar.gz
```

Once the tarball is extracted, change directories to the newly created source folder:

```bash
cd mod_auth_mysql-2.9.0
```

To build the module from the downloaded source code, you're actually going to use Apache's **apxs** command directly. Execute the following command, using the path to your **apxs** binary on your system; the default Apache location of `/usr/local/apache2/bin` is used here:

```bash
/usr/local/apache2/bin/apxs -c -i mysqlclient -lm -l2 mod_auth_mysql.c
```

If the build is successful, you should see a couple of compilation lines, and no errors. If, instead, you get an error about a missing **mysql.h** file, and a whole slew of **MySQL**-related errors, you might need to manually specify the paths to the **MySQL** libraries and include files. Using the default locations from **MySQL**, your command might instead look like this:

```bash
/usr/local/apache2/bin/apxs -c -i mysqlclient -lm -l2 \
-L /usr/local/mysql/lib/mysql \
-I /usr/local/mysql/include/mysql \
mod_auth_mysql.c
```

To install the newly compiled module, you’ll need to execute the following command as root. As usual, change the path to `apxs` to point to your `apxs` binary:

```bash
/usr/local/apache2/bin/apxs -i mod_auth_mysql.la
```

The next installation task you need to perform is to add the necessary command to load the module in `httpd.conf`. To do this, open your `httpd.conf` file, find a suitable location to add a module definition — usually at the very end of the configuration file, or next to other `LoadModule` statements — and add the following:

```apache
LoadModule mysql_auth_module modules/mod_auth_mysql.so
```

Finally, restart Apache.

## Configuration and Usage

Once you have your database tables ready and modules installed, all that remains is to tell Apache what needs to be protected. Like standard Apache basic authentication, you’ll need to add some configuration directives to either a `<Directory>` section in `httpd.conf`, or create a `.htaccess` file in the directory you choose to protect.

Telling Apache to validate user credentials against your MySQL database would usually involve the following at a minimum:

- `AuthName "<zone name>"`
- `AuthType Basic`
- `AuthMySQLDB dbname`
- `AuthMySQLUser userid`
- `AuthMySQLPassword password`
- `AuthMySQLEnable On`
- `Require valid-user`

The first two lines and the last line of these directives should already be familiar to you. They simply define the name of the protected area, the type of authentication, and that any valid user found in the checked resource is allowed access. The other lines tell Apache where to find the authentication information. Instead of giving Apache the name of a file that contains the passwords for each valid user, you’re supplying database information — database name, username, and password — so that Apache and mod_auth_mysql know where to look. The sixth line, `AuthMySQLEnable On` simply tells Apache to actually use mod_auth_mysql — it’s a way to disable MySQL authentication without having to completely unload or remove the module.

To use the authentication tables you created earlier, you would add the following in your `<Directory>` or `.htaccess` definitions:

- `AuthName "MySQLAuth"`
- `AuthType Basic`
- `AuthMySQLDB apacheauth`
- `AuthMySQLUser apache`
- `AuthMySQLPassword apache`
- `AuthMySQLEnable On`
- `AuthMySQLPwEncryption sha1`
- `Require valid-user`
