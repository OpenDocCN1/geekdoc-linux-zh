# Frequently Asked Questions

The following Frequently Asked Questions, answered by the authors of this book, are designed to measure your understanding of the concepts presented in this chapter and to assist you with real-life implementation of these concepts. To have your questions about this chapter answered by the author, browse to www.syngress.com/solutions and click on the “Ask the Author” form.

Q: Data is encrypted when I use Query Analyzer to communicate with my database? If not, are there secure ways to administer a server?

A: If you install a certificate on the server that is trusted by the client, you can establish an SSL connection with the server (SQL 2000 only) for a secure session. If SSL is not an option, you could make use of either IPsec, PPTP, or a third-party encryption product (such as www.stunnel) to establish a secure tunnel to the SQL Server.

Q: How do I encrypt data in SQL Server?

A: Your best is to encrypt the data before placing it into your database and decrypt the data once you read it again. One reason this strategy advantageous is that you keep the encryption key from being stored on the SQL Server. It is a pretty weak strategy to allow SQL Server itself to be responsible for both the encryption and storage of the data since if your SQL Server is compromised it likely both the data and the key will fall into the attacker's hands. My recommended strategy for encrypting data is to use public encryption by placing a public key on the machine performing the encryption and then storing the private key in a secure location not accessible to the Web or SQL Servers in your environment. The secured server with the private keys can periodically poll the production server for ciphertext when the data needs to be decrypted.

Q: How do I require SSL encryption for all clients?

A: From a high level, in order to enable encryption you must install a server certificate on the SQL Server and select the Force Protocol Encryption option box in the Server Network Utility. In order to install a certificate on the server, you can either install Certificate Services on a machine in your network to issue a certificate to the SQL Server or request a certificate using

![](bbox=[0.07, 0.943, 0.296, 0.973])