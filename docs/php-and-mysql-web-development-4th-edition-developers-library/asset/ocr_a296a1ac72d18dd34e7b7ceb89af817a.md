As an alternative to listing SSL options in the option file, you can specify them on the command line. For example, in the directory where the SSL files are located, I might invoke mysql like this (enter the command all on one line):

```
```
% mysql --ssl-ca=ca-cert.pem --ssl-cert=client-cert.pem
        --ssl-key=client-key.pem
```
```

However, all that typing is burdensome to do often.

The certificate and key files in the *samppd* distribution suffice to enable you to establish encrypted connections. However, they're publicly available (anyone can get the distribution), so connections thus established cannot truly be said to be secure. After you use these files to verify that SSL is working properly, you should replace them with ones that you generate yourself. For instructions on making your own certificate and key files, see the *sssl/README.txt* file in the *samppd* distribution. You may also want to consider purchasing a commercial certificate.

The discussion thus far describes how any account can use SSL on an optional basis. You can also set up an account to disallow unencrypted connections and require it to use SSL. This can be done for a new or existing account.

If you use *GRANT* to create a new account, add a *REQUIRE* clause that specifies the constraints that connections must satisfy. Suppose that you want to set up a user named *laura* who will be connecting to the server on *cobra.snake.net* from the host *rat.snake.net* to access the *finance* database. To require only that connections be encrypted, use this statement:

```
```
GRANT ALL ON finance.* TO 'laura'@'rat.snake.net'
IDENTIFIED BY 'moneymoneymoney'
REQUIRE SSL;
```
```

For more security, use *REQUIRE X509* instead. In that case, *laura* must supply a valid X509 client certificate when connecting. (This will be the file named by the *--ssl-cert* option.) As long as the certificate is valid, its contents don't otherwise matter. To require specific certificate contents, use some combination of *CIPHER*, *ISSUER*, and *SUBJECT* in the *REQUIRE* clause. *CIPHER* indicates the type of encryption method you want the connection to use. *ISSUER* or *SUBJECT* indicate that the client certificate must have been issued by a particular source or for a particular recipient. These clauses narrow the scope of otherwise-valid certificates to include only those with specific content. The following *GRANT* statement requires a particular issuer in the client certificate and specifies the use of *EXP1024-RC4-SHA* encryption:

```
```
GRANT ALL ON finance.* TO 'laura'@'rat.snake.net'
IDENTIFIED BY 'moneymoneymoney'
REQUIRE ISSUER '/C=US/ST=WI/L=Madison/O=samppd/OU=CA/CN=samppd'
CIPHER 'EXP1024-RC4-SHA';
```
```

To modify an existing account to require SSL connections, use a *GRANT USAGE* statement of the following form, where *require_options* specifies the SSL characteristics that you want to enforce: