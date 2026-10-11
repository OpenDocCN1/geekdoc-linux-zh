work to be done. Even if the details are many and intricate, these programs make everything seem trivial. In this chapter, we cover using the tools just mentioned as well as some of the manual processes of account creation.

# # Storing user information

The basic user database is stored in the /etc/passwd file, which lists all valid user names and their associated information. The file has one line per user name and is divided into seven colon-delimited fields:

+   - User name, up to eight characters maximum. The user name is case-sensitive and is usually all lower-case.
+   - Password, in encrypted form. If shadow passwords are used, an x will appear here.
+   - Numeric user id.
+   - Numeric group id. This usually matches the user id.
+   - Full name or other description of account.
+   - The user's home directory, which is usually /home/username.
+   - Login shell (program to run at login).

Any user on the system may read the password file, so that they can, for example, learn the name of another user. This means that the password (the second field) is also available to everyone. The password file contains the password, so in theory there is no problem. However, the encryption is breakable, especially if the pass- word is weak (for example, it is short or it can be found in a dictionary). Therefore, it is not a good idea to have the password file in the password file.

Linux systems have shadow passwords to help solve this problem. This is an alter- native way of storing the password: the encrypted password is stored in a separate file, /etc/shadow, which only root can read. The /etc/passwd file only contains a special marker, displayed as an x, in the second field. Any program that needs to verify a user is setuid, which allows the program to run as a specified user id, and can therefore access the shadow password file. Normal programs, which only use the other fields in the password file, can't get at the password.

![](bbox=[0.1, 0.78, 0.2, 0.82])

Shadow passwords are discussed in more detail later in this chapter and in Chapter 17.

The /etc/passwd file contains a number of user and service accounts. The service accounts are installed by default to allow the various services to function properly. Following is a sample /etc/passwd file: