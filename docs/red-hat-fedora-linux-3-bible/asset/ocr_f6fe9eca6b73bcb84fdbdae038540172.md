# Using the “r” commands: rlogin, rcp, and rsh

The rlogin, rcp, and rsh commands all use the same underlying security mechanism to enable remote login, remote file copy, and remote execution, respectively, among computers. These commands are included with Fedora Core to be compatible with legacy UNIX systems. Because “r” commands are inherently insecure, however, most people use ssh and scp commands to provide the same functionality in a more secure way.

> **CROSS REFERENCE:** For a description of these “r” commands, refer to the *Red Hat Linux Bible* Web site at Wiley Publishing: www.wiley.com/go/fedora3bible.

# Summary

Most use of the World Wide Web centers on the Web browser. Mozilla is popular with Fedora Core, and is accessible from a button on your desktop. The e-mail program that comes with Mozilla, called Mozilla Mail, provides almost everything you need for reading, sending, and managing your mail. Ximian Evolution, which can also be used for managing your e-mail, is now the preferred mail reader for Fedora Core. To read newsgroups, you can also use Mozilla or the Pan newsreader.

Commands such as *telnet* (for remote login) and *ftp* (for remote file copying) are available for communicating with remote computers from the command line in Fedora Core. There are also improved programs for remote login and file copy, such as *ssh*, *scp*, and *ncftp*.