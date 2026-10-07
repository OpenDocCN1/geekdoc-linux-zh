network if the remote machine is directly reachable. To use FTP, start the FTP client software and provide the name of the remote system you want to connect to. For example, assuming you can get to the remote machine through a LAN or the Internet (which knows about the remote machine thanks to Domain Name Service), issue the following command:

```
`ftp chattou.com`
```

This instructs your FTP software to try to connect to the remote machine chattou.com and establish an FTP session.

When the connection is completed (and assuming the remote system allows FTP logins), the remote prompts for a userID. If anonymous FTP is supported on the system, a message usually tells you exactly that. The following is for the Linux FTP archive site sunsite.unc.edu:

```
```text
ftp sunsite.unc.edu
331 Guest login ok, send your complete e-mail address as password.
Enter username (default: anonymous): anonymous
Enter password [tparker@tpci.com]:
;FTP; Open
230-                WELCOME to UNC and SUN's anonymous ftp server
230-                University of North Carolina
230-                Office FOR Information Technology
230-                SunSITE.unc.edu
230 Guest login ok, access restrictions apply.
FTP>
```

```

After the login process is completed, you see the prompt FTP> indicating the remote system is ready to accept commands.

When you log on to some systems, you may see a short message that contains instructions for downloading files, any restrictions that are placed on you as an anonymous FTP user, or information about the location of useful files. For example, you may see messages like these (taken from the Linux FTP site):

```
```text
To get a binary file, type: BINARY and then: GET "File.Name" newfilename
To get a text file, type: ASCII and then: GET "File.Name" newfilename
Names MUST match upper, lower case exactly. Use the "quotes" as shown.
To get a directory, type: DIR. To change directory, type: CD "Dir.Name"
To read a short text file, type: GET "File.Name" TT
For more, type HELP or see FAQ in gopher.
To quit, type EXIT or Control-Z.
```

```

```
```text
230- If you email to info@sunsite.unc.edu you will be sent help
=information
230- about how to use the different services sunsite provides.
230- We use the WuarCmive experimental ftpd. if you "get"
```

```