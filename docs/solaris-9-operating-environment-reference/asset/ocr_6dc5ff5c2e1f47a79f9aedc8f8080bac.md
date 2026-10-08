The following example establishes an ftp connection from the system oak to the system elm specifies ASCII format, gets the file quest from elm, puts it into the /tmp/quest directory on oak, and quits the session.

```
oak$ ftp
ft> open elm
Connected to elm
220 elm FTP server (UNIX(r)System V Release 4.0) ready.
```

```
Name (elm:ignatz): ignatz
331 Password required for ignatz.
Password:
230 User ignatz logged in.
```

```
ftp> asc
ft> get quest /tmp/quest
200 PORT command successful.
150 ASCII data connection for /tmp/quest (129.144.52.119,1333)
226 Transfer complete.
```

```
ftp> quit
221 Goodbye.
oak$
```

Note — Correct execution of many commands depends on proper behavior by the remote server.

An error in the treatment of Returns in the 4.2 BSD code that handles transfers with a representation type of network ASCII has been corrected. This correction may result in incorrect transfers of binary files to and 4.2 BSD servers using a representation type of network ASCII. Avoid the problem by using the image type.

Failure to login can result from an explicit deny by the remote FTP server because the account is listed in /etc/ftpusers. See in.ftp(1M) and ftpusers(4) in the Solaris 8 release.

# Options

You can specify the following options for the ftp command either or to the ftp command interpreter.

+   -d Enable debugging.
-g Disable filename globbing.
-i Turn off interactive prompting during multiple file transfers.
-n Do not auto-login on initial connection. If auto-login is not disabled, ftp checks the .netrc file in the user's home directory for an entry describing an account on a remote machine. If no entry exists, ftp prompts for the login name of the account on the remote machine (the default is the login name on the local machine) and, if necessary, prompts for a password and an account with which to log in.
-t Enable packet tracing (unimplemented).