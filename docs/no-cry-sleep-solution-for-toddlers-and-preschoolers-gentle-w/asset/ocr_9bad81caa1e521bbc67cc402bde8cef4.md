> NOTE On Red Hat, you can use the vsftpd RPM package to set up the home directory and the copies of the system directories. If you do not have access to the vsftpd package, you may have to create these system directories yourself.

# The FTP User Account: anonymous

To allow anonymous FTP access by other users to your system, you must have a user account named FTP. Most distributions already create this account for you. If your system does not have such an account, you will have to create one. You can then place restrictions on the FTP account to keep any remote FTP users from accessing any other part of your system. You must also modify the entry for this account in your /etc/passwd file to prevent normal user access to it. The following is the entry you find in your /etc/passwd file on Red Hat systems that sets up an FTP login as an anonymous user:

```
ftp:x:14:50:FTP User:/var/ftp: 
```

The x in the password field blocks the account, which prevents any other users from gaining access to it, thereby gaining control over its files or access to other parts of your system. The user ID, 14, is a unique ID. The comment field is FTP User. The login directory is /var/ftp. When FTP users log in to your system, they are placed in this directory. If a home directory has not been set up, create one and then change its ownership to the FTP user with the chown command.

# FTP Group

The group ID is the ID of the ftp group, which is set up only for anonymous FTP users. You can set up restrictions on the ftp group, thereby restricting any anonymous FTP users. Here is the entry for the ftp group you find in the /etc/group file. If your system does not have one, you should add it:

```
ftp::50:
```

# Creating New FTP Users

If you are creating virtual FTP hosts, you will need to create an FTP user for each one, along with its directories. For example, to create an FTP server for a host1-ftp host, you would create a host1-ftp user with its own directory.

```
useradd -d /var/host1-ftp host1-ftp
```