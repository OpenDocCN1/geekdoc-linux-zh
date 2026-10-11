+------------------------+
| Variable_name | Value |
+------------------------+
| have_ssl | DISABLED |
+------------------------+

If you see DISABLED or YES, SSL support is available. DISABLED means that support is present but has not yet been enabled. That’s okay; the files necessary to enable SSL are discussed next.

With a MySQL installation that includes SSL support, the server and its clients can communicate securely. Each end of a connection uses three files to set up secure communications:

+   A Certificate Authority (CA) certificate. A CA is a trusted third party; its certificate is used to verify the authenticity of the client and server certificates. It’s common to purchase a CA certificate from a commercial entity, but you can generate your own.
+   A certificate file that authenticates one side of the connection to the other.
+   A key file, used to encrypt and decrypt traffic over the connection.

The server’s certificate and key files must be installed first. If you don’t have files if your own, the ssl directory of the samDB distribution contains some boilerplate files that you can use:

+   ca-cert.pem, the Certificate Authority certificate
+   server-cert.pem, the server’s certificate
+   server-key.pem, the server’s public key

Copy these three files to your server’s data directory, and then add some lines to the [mysqld] group of an option file that the server reads when it starts, such as /etc/my.cnf on Unix or c:\my.ini on Windows. The options should indicate the path-names to the certificate and key files. For example, if the data directory is /usr/local/mysql/data, list the options like this:

```
[mysqld]
ssl-ca=/usr/local/mysql/data/ca-cert.pem
ssl-cert=/usr/local/mysql/data/server-cert.pem
ssl-keys=/usr/local/mysql/data/server-key.pem
```

You can put the certificate and key files elsewhere if you like, but the location should be one to which only the server has access. After you install the SSL files and modify the option file, restart the server.