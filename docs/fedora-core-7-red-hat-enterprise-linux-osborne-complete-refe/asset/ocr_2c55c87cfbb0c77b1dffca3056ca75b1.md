are installing an FTP server yourself, you need to know the procedures detailed in the following sections to install an FTP server and create its data directories.

The **vsftpd** FTP package does not create a directory where users can upload files to the FTP site. Such a directory is usually named the *incoming* directory, located at **ftp/pub/incoming**. If you want such a directory, you will have to create it, make it part of the **ftp** group, and then set its permissions to allow users write access.

```
# chgrp ftp /var/ftp/pub/incoming
# chmod g+w /var/ftp/pub/incoming
```

# ## FTP Users

Normal users with accounts on an FTP server can gain full FTP access simply by logging into their accounts. Such users can access and transfer files directly from their own accounts or any directories they may have access to. You can also create users, known as guest users, that have restricted access to the FTP publicly accessible directories. This involves setting standard user restrictions, with the FTP public directory as their home directory. Users can also log in as anonymous users, allowing anyone on the network or Internet to access files on an FTP server.

# ## Anonymous FTP: vsftpd

An anonymous FTP site is essentially a special kind of user on your system with publicly accessible directories and files in its home directory. Anyone can log in to this account and access its files. Because anyone can log in to an anonymous FTP account, you must be careful to restrict a remote FTP user to only the files on that anonymous FTP directory. Normally, a user’s files are interconnected to the entire file structure of your system. Normal users have write access that lets them create or delete files and directories. The anonymous FTP files and directories can be configured in such a way that the rest of the file system is hidden from them and remote users are given only read access. In ProFTPD, this is achieved through configuration directives placed in its configuration file. An older approach implemented by the vsftpd package involves having copies of certain system configuration, command, and library files placed within subdirectories of the FTP home directory. Restrictions placed on those subdirectories then control access by other users. Within the FTP home directory, you then have a publicly accessible directory that holds the files you want to make available to remote users. This directory usually has the name **pub**, for public.

An FTP site is made up of an FTP user account, an FTP home directory, and certain copies of system directories containing selected configuration and support files. Newer FTP daemons, such as ProFTPD, do not need the system directories and support files. Most distributions, including Fedora and Red Hat, have already set up an FTP user account when you installed your system.

> **Note** The *vsftpd* RPM package will set up the home directory and the copies of the system directories when it is installed. If, for some reason, you do not want to use the *vsftpd* RPM package (if, for instance, you are recompiling the source code), you may have to create these system directories yourself.