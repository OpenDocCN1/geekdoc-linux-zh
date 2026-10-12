
## FTP user types

As an administrator of an FTP server, it is your responsibility to make sure that you share your files in a way that gives people access to the information that you want them to have without compromising the security of your system. This means implementing a strong security policy and relentlessly monitoring the system to prevent abuse.

> **CROSS-REFERENCE:** See Chapter 14 for information on computer security issues.

Several different types of users can log in to and use an FTP server. The user name *anonymous* is the most common for providing public access. **Real users** represent the category of users who have real login accounts to the Red Hat Linux system that contains your FTP server (that is, you know them and have given them permission for other uses besides FTP). A guest user is similar to a real user account, except that the guest user access to the computer’s file system is more restricted. Procedures for setting up these different kinds of users for each of the two FTP servers described here are outlined later in this chapter.

At this point, you need to decide if you want to run the WU-FTPD or vsFTpd server on your Red Hat Linux system. The one that you choose will, by default, take over the full functions of FTP service on your computer.

## Using the Washington University FTP Server (WU-FTPD)

To set up Washington University FTP Server software, you should first make sure that the wu-ftpd and anonftp software packages are installed. When wu-ftpd is first installed, it is disabled. However, much of the FTP configuration is already in place.

> **NOTE:** Refer to the “Starting and shutting down the WU-FTPD service” section for information on enabling and starting your FTP server.

The following sections describe the setup of the wu-ftpd package when it is first installed:

### FTP Daemon

- The FTP daemon is set up in the `/etc/xinetd.d/wu-ftpd` file as `/usr/sbin/in.ftpd`. When someone requests FTP service from your computer (probably on port 21), the xinetd daemon (which listens to lots of ports) starts the FTP daemon to handle that FTP login request. The daemon runs with the -l option (so that FTP requests are logged by syslog to `/var/log/messages`) and the -a option (so that the `/etc/ftpdaccess` file is used to define access permissions).

### Access Permissions (`/etc/ftpdaccess`)

- The ftpaccess file delivered with the wu-ftpd package is quite restrictive, although you can change it to be as open or as restrictive as you like. Here is how the file is originally set:

```text
deny-uid %-99 %65534-  
deny-gid %-99 %65534-  
allow-uid ftp  
allow-gid ftp
```

The deny-uid and deny-gid entries prevent access to the FTP service from any users with IDs that are 99 or less or 65534 or greater for either user or group accounts. The allow-uid and allow-gid lines make an exception to the deny rules by allowing the ftp user and group to use the FTP service.

- **guestuser \*** — This line causes all users to have their home directory as their root directory by default. So, if your home directory were /home/jake and you opened an FTP connection to the computer, you would only be able to see files that were in /home/jake or its subdirectories. (To change this behavior, either add a comment character, #, before the line or add a realuser user line, replacing user with the name of the user whom you want to allow to change directories outside of his/her home directory.)

- **email root@localhost** — E-mail related to the administration of the FTP server is directed to the root user on the local computer, by default.

- **loginfails 5** — The FTP connection terminates after five consecutive failed login attempts. (This slows down people who are trying to guess your server’s passwords.)

- **readme README\*** — When the user logs in (login) or changes to any other accessible directory (cwd=*), the user is notified of the existence of README files, if they exist. By default, no README files exist. For any file that begins with the word README, a message is displayed by the server that says “Please read the file README.whatever.”

- **message** — This indicates that the message contained in the /welcome.msg file should be displayed when a user logs in to FTP. A similar line indicates that the .message file is displayed when the user enters a directory that contains such a file. By default, none of these files exists. If you want them on your FTP server, you have to create them yourself.

> **NOTE:** The /welcome.msg file is relative to the root directory that the FTP user logs into. A guest user, such as anonymous, would by default have /var/ftp as his or her root directory. The welcome.msg file would therefore have to be in /var/ftp.

- **compress yes all** — This enables compression of files for the FTP site for all users. The compress command is the standard compression command used in UNIX systems (though gzip is used more often with free operating systems, such as Linux). The compress command lines used to carry out the compressions are defined in /etc/ftpconversions. (Files stored by compress have a .Z suffix.)

- **tar yes all** — This enables tar compression for all users at the FTP site. The tar command is the standard UNIX command used to create archives of multiple files. The tar commands used to carry out the compressions are defined in /etc/ftpconversions. (Files stored by tar have a .tar, .tar.gz, or .tar.Z suffix.)

- **chmod no guest, anonymous** — This prevents guest and anonymous user names from changing the permissions on any files or directories.

- **delete no anonymous** — This prevents anonymous user name from deleting files or directories.

- **overwrite no anonymous** — This prevents anonymous user name from overwriting existing files or directories.

- **rename no anonymous** — This prevents anonymous user name from renaming any files or directories.

- **log transfers anonymous, guest, real inbound, outbound** — This logs file transfers for the anonymous user, guest user, and any real users (that is, those who have their own user accounts on the Linux system). Both uploads (inbound) and downloads (outbound) transfers are logged.

- **shutdown /etc/shutmsg** — This checks the /etc/shutmsg file to see if the server is about to be shut down. If it is, your FTP server sends a message to current FTP users, warning them that the server is about to go down. It also denies new FTP connections and disconnects current users at a specified time prior to shutdown. (By default, the /etc/shutmsg file does not exist.) See the section on setting up FTP shutdowns later in this chapter for information on how to set up a shutdown file for scheduled FTP shutdowns.

- **passwd-check rfc822 warn** — This checks that passwords for anonymous logins are rfc822-compliant addresses. In other words, the FTP server asks for any valid e-mail address as the password for the anonymous login. If the address is not compliant (that is, is not in the form user@host.domain), the server will “warn” the user but still allow the user to log in.

### FTP Root Directory

- For a user who logs in as an anonymous user, the /var/ftp directory is assigned as the user’s root directory. In other words, the anonymous user could not cd above the /var/ftp directory (or even know what files exist outside the /var/ftp directory structure).

Within the /var/ftp directory are those directories and files necessary to make FTP work properly, without your having to access other files in the file system. The /bin directory contains executable commands that FTP may need (such as compress, ls, and gzip). The /etc directory contains passwd and group entries. The /lib directory holds shared object libraries needed by FTP. Finally, the /pub directory is available for placing the files that you want to be generally available to anonymous users.
