# Frequently Asked Questions

The following Frequently Asked Questions, answered by the authors of this book, are designed to measure your understanding of the concepts presented in this chapter and to assist you with real-life implementation of these concepts. To have any of your questions about this chapter answered by the author, browse to **www.syngress.com/solutions** and click on the "Ask the Author" form.

+   Q: Which is more secure: Microsoft SQL Server or Oracle?
A: Neither. They're as good and as bad as each other. I often hear that people are migrating from SQL Server to Oracle because of Microsoft's security failures, but Oracle has a similar record.

+   Q: What about Oracle's "unbreakable" marketing campaign?
A: According to sources high in Oracle, this campaign speaks not of security but of the business being unbreakable when using Clusters. 100 percent uptime means the "business" is unbreakable. Furthermore, the campaign tags Oracle's commitment to security. Versions of Oracle have undergone 14 independent security evaluations and passed. The current version has not yet passed.

+   Q: Why can I no longer connect as "internal"?
A: This feature has been disabled in Oracle 9i.

+   Q: How are Oracle passwords encrypted?
A: Oracle passwords are encrypted using the Data Encryption Standard (DES) algorithm to create eight-byte hashes stored in the table SYS.USER. To create the hash, the username and the password are appended together and broken up into eight-byte pieces. The first eight bytes of the password are used as a key to DES encrypt the magic number 0x123456789ABCDEF resulting bytes are then encrypted with the next bytes of the username/password, resulting in a new eight-byte value. This process is repeated until the entire username/password has been used.

One interesting characteristic to note is the "salt" used to create the hash. The salt is the username. This adds additional security in that different users with the same passwords will have different hashes. However, it falls short of a true salt in the same password will always have hash to the value when used by the same user.

![](bbox=[0.335, 0.535, 0.662, 0.835])