
## Getting Files from the Internet with ftp

Some of the Internet's great information resources are FTP sites, which contain hundreds of thousands of files from all over the Internet. FTP sites are similar to Web sites, but are directory-oriented and speak a different protocol. They're less fun than the Web usually is but often more practical.

One of the easiest ways to access information on FTP sites is to use anonymous ftp, which lets you access the sites and download files to your computer (Code Listing 12.2 shown on the next page).

### Getting a single file through anonymous ftp:

- 1. `ftp calvin.raycomm.com`

  At the shell prompt, type `ftp` followed by the name of the FTP site to which you're connecting. Of course, if the computer has an IP number but no name, type the IP number instead. You'll be prompted to log in, as shown in Code Listing 12.2.

- 2. `anonymous`

  For the user name, type `anonymous`. (Type `ftp` if you get tired of typing `anonymous`—it nearly always works.)

- 3. `you@wherever.com`

  Use your email address for the password. It's polite to identify yourself to the people who provide the FTP service. Just `you@` is usually sufficient.

- 4. `cd /pub/files`

  Use standard Unix `cd` commands to move through the directory tree to the file you want.

```text
[ejr@hobbes ejr]$ ftp calvin.raycomm.com
Connected to calvin.raycomm.com.
220 calvin Microsoft FTP Service (Version 2.0).
Name (calvin.raycomm.com: ejr): anonymous
331 Anonymous access allowed, send identity (e-mail name) as password.
Password:
230 Anonymous user logged in.
Remote system type is Windows_NT.
ftp> cd /pub/files
250 CWD command successful.
ftp> binary
200 Type set to I.
ftp> hash
Hash mark printing on (1024 bytes/hash mark).
ftp> get jokearchive.gz
local: jokearchive.gz remote: jokearchive.gz
200 PORT command successful.
150 Opening BINARY mode data connection for jokearchive.gz (1481035 bytes).
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######################################################################
######
226 Transfer complete.
1481035 bytes received in 4.07 secs (3.6e+02 Kbytes/sec)
ftp> quit
221
```

**Code Listing 12.2** Use anonymous ftp to get files from archives across the Internet.
