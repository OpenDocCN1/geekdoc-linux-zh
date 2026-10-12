HTTP is a stateless protocol; each request sent to the server and each response are handled individually, and not in an intelligent fashion. Therefore, the authentication information must be included with each request. That means each request to a password-protected area is larger and therefore somewhat slower. To avoid unnecessary system use and delays, protect only those areas of your website that absolutely need protection.

To use Basic Authentication, you need a file that lists which users are allowed to access the resources. This file is composed of a plain text list containing name and password pairs. It looks very much like the `/etc/passwd` user file of your Linux system.

**CAUTION**

Don't use `/etc/passwd` as a user list for authentication. When you're using Basic Authentication, passwords and usernames are sent as base 64-encoded text from the client to the server—which is just as readable as plain text. The username and password are included in each request that is sent to the server. So, anyone who might be snooping on Net traffic would be able to get this information!

To create a user file for Apache, use the htpasswd command. This is included with the Apache package. If you installed using the RPMs, it is in `/usr/bin`. Running htpasswd without any options produces the following output:

Usage:
`htpasswd [-c|mdps] passwordfile username`
`htpasswd -b[-cmdps] passwordfile username password`

`htpasswd -n[mdps] username`
`htpasswd -nb[mdps] username password`

+   -c Create a new file.
+   -n Don't update file; display results on stdout.
+   -m Force MD5 encryption of the password.
+   -d Force CRYPT encryption of the password (default).
+   -p Do not encrypt the password (plaintext).
+   -s Force SHA encryption of the password.
+   -b Use the password from the command line rather than prompting for it.
+   -D Delete the specified user.

On Windows, TPF and NetWare systems the `-m` flag is used by default.
On all other systems, the `-p` flag will probably not work.

As you can see, it isn't a very difficult command to use. For example, to create a new user file named gnulixusers with a user named wsb, you need to do something like this:
`# htpasswd -c gnulixusers wsb`

You would then be prompted for a password for the user. To add more users, you would repeat the same procedure, only omitting the `-c` flag.