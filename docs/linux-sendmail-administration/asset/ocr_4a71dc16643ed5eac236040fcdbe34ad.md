# Sendmail Security Protocols 351

These essential pieces of information must be identified to Sendmail in the configuration. The path to the directory where certificates are stored is defined by the confCACERT_PATH parameter, and the certificate for a single CA is defined using the confCACERT parameter. Both can be used in the m4 configuration file—for example:

```
define(`confCACERT_PATH`, `/etc/httpd/conf/ssl1.crt`)`
define(`confCACERT`, `/etc/httpd/conf/ssl1.verisgn.crt`)
```

In this example, we use the same certificate directory that was set up for the Apache server on our system. This is, however, completely arbitrary. Certificates can be stored anywhere as long as the directory and the certificates in the directory can be written by root.

n addition to information about CA certificates, Sendmail needs to know the public and private keys it should use to identify and encrypt its own communication. Sendmail uses a different set of public and private keys to define whether it is acting as a server or a client. These values are defined by four m4 parameters:

confSERVER_CERT This parameter sets a value for the ServerCertFile option.
ServerCertFile identifies the file that contains the X.509 certificate used when Sendmail acts as a server. In effect, this is the server's public key. For example:

onfSERVER_KEY This parameter sets a value for the ServerKeyFile option.
ServerKeyFile identifies the file that contains the private key used when Sendmail acts as a server. The confSERVER_KEY parameter could be defined as follows:

```
define(`confSERVER_KEY`, `/etc/httpd/conf/ssl1.server.key`)
```

onfCLIENT_CERT This parameter sets a value for the ClientCertFile option.
ClientCertFile identifies the file that contains the X.509 certificate used when Sendmail acts as a client. In effect, this is the client's public key. The following example points to a certificate in the Apache SSL directory:

```
define(`confCLIENT_CERT`, `/etc/httpd/conf/ssl1.client.crt`)
```

onfCLIENT_KEY This parameter sets a value for the ClientKeyFile option.
ClientKeyFile identifies the file that contains the private key used when Sendmail acts as a client. The following command tells Sendmail where the client's private key is stored:

```
define(`confCLIENT_KEY`, `/etc/httpd/conf/ssl1.client.key`)
```

In the examples above, we used the same certificates and keys for Sendmail that we used for Apache. This is possible, but only if you run Sendmail and Apache on the same server.

![](bbox=[0.915, 0.577, 0.985, 0.697])