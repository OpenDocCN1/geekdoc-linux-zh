
By default, Ubuntu doesn't activate the Apache SSL module that allows you to use encryption when transmitting web pages. The SSL module requires that you have a valid certificate to use for encryption.

You can purchase a certificate from an authorized certificate authority (CA) or you can create your own self-signed certificate using the OpenSSL package if you selected to install SSL during the Ubuntu server installation process.

To create a self-signed certificate, follow these steps:

- 1. **Generate a key for the certificate using the command:**
  ```
  openssl genrsa -des3 -out server.key 1024
  ```
  Enter a passphrase to protect the key from unauthorized modification.
- 2. **Generate a certificate signing request (CSR), which is used to identify you and your server for the certificate. Do this using the command:**
  ```
  openssl req -new -key server.key -out server.csr
  ```
  The server.key file you created in step 1 must be in the folder where you run this command from. This command will ask questions about your name, organization, and server information. This information will be used in your certificate to identify you to your customers.
- 3. **Create the self-signed certificate using the command:**
  ```
  openssl x509 -req -days 365 -in server.csr -signkey server.key -out server.crt
  ```
  The server.key and server.csr files you previously generated must be in the same folder where you run this command from.
- 4. **Copy the key and certificate to the server /etc/ssl folder locations:**
  ```
  sudo cp server.key /etc/ssl/private
  sudo cp server.crt /etc/ssl/certs
  ```
- 5. **Specify the file locations in the default-ssl virtual host configuration lines for the web host:**
  ```
  SSLCertificateFile /etc/ssl/certs/server.crt
  SSLCertificateKeyFile /etc/ssl/private/server.key
  ```
- 6. **Enable the SSL module in Apache:**
  ```
  sudo a2enmod ssl
  ```
- 7. **Add the default-ssl virtual host to the enabled sites using the command:**
  ```
  sudo a2ensite default-ssl
  ```

Now you should be able to connect using the HTTPS protocol to your web site. When you use a self-signed certificate, most web browsers will produce a warning message indicating that there's a security risk involved with accepting a self-signed certificate from a web server. Self-signed certificates shouldn't be used in a production environment, as it forces your customers to accept you as the signing authority.

## The MySQL Software

A main component of a successful dynamic web page environment is a database for storing and accessing data. The most popular database platform used in the open-source world is the MySQL database server.

Much of the popularity of MySQL comes from it being the original default database used in the PHP programming language (however, PHP can now interface with many different database packages), as well as the speed of the MySQL database server.

The original MySQL database server was well known for being fast but not overly robust. It lacked many of the advanced features commonly found in commercial databases, such as transactions, foreign keys, and row-level record locking.

To solve this problem, the developers at MySQL redesigned MySQL to work with multiple storage engines. A storage engine is the core of the database server. It handles the database interface—storing, managing, and deleting data for the server.

MySQL now supports several different types of storage engines, each one with a different specialty. Table 21-3 lists the different storage engines available in MySQL.

| Table 21-3: The MySQL Storage Engines |
| Engine | Description |
| MyISAM | The original storage engine; speedy, but lacking many advanced database features |
| InnoDB | The newest, full-featured storage engine; although it supports many commercial-quality features, it's significantly slower than the MyISAM storage engine |
| Memory | Provides tables in memory |
| Merge | Combines multiple MyISAM tables into a single table |
| CSV | Stores data as comma-separated values in text files |

Many high-volume web application sites still use the original MyISAM storage engine for its speed qualities, forsaking advanced features for performance.

The following sections describe how to use the MySQL database server installed on the Ubuntu server.

## Accessing the Server

On the Ubuntu server you access the MySQL server via a command-line interface tool. The mysql program allows you to connect to the MySQL server, execute SQL commands, and view the results.

To connect to the default MySQL database using the root user account, type

```
mysql -u root -p
```

After entering the password, you should be at the MySQL prompt:

```
$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor. Commands end with : or \g.
```
