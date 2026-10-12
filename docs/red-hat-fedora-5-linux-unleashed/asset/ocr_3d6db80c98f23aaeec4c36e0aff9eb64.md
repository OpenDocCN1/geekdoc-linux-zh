The welcome.msg file is not created with the installation of the RPM, but you can create it using a text editor. Type the following:

```
Welcome to the anonymous ftp service on %L!

There are %N out of %M users logged in.

Current system time is %T

Please send email to %E if there are
any problems with this service.

Your current working directory is %C
```

Save this file as /var/ftp/welcome.msg. Verify that it works by connecting to the FTP server:

```
220 FTP server ready.
504 AUTH GSSAPI not supported.
504 AUTH KERBEROS_V4 not supported.
KERBEROS_V4 rejected as an authentication type
Name (shuttle:phduson): anonymous
331 Guest login ok, send your complete e-mail address as password.
Password:
230- Welcome to the anonymous ftp service on shuttle.home.org!
230-
230- There are 1 out of unlimited users logged in.
230-
230- Current system time is Mon Nov 3 10:57:06 2003
230-
230- Please send email to root@localhost if there are
230-any problems with this service.
230-Your current working directory is /
```

# Display Administrator's Email Address

This line sets the email address for the FTP administrator:

```
email <name>
```

This string is printed whenever the %E magic cookie is specified. This magic cookie is used in the message line or in the shutdown file. You should display this string to users in the login banner message so that they know how to contact you (the administrator) in case of problems with the FTP server.