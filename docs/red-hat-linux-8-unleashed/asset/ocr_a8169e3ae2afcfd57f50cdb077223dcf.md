# CHAPTER 16 Apache Web Server Management

To use Basic authentication, you need a file that lists which users are allowed to access the resources. This file is composed of a plain text list containing name and password pairs. It looks very much like the /etc/passwd user file of your Linux system.

> CAUTION Don't use /etc/passwd as a user list for authentication. When you're using Basic authentication, passwords and usernames are set as base64-encoded text from the client to the server—which is just as readable as plain text. The username and password are included in each request that is sent to the server. So, anyone who might be snooping on Net traffic would be able to get this information!

To create a user file for Apache, use the htpasswd command. This is included with the Apache package. If you installed the RPMs, it's in /usr/bin. Running htpasswd without any options will produce the following output:

Usage:

```
htpasswd [-cmds passwordfile username
htpasswd -b [-cmds] passwordfile username password
```

```
htpasswd -n[mdps] username
htpasswd -nb[mdps] username password
-c Create a new file.
-n Don't update file; display results on stdout.
-m Force MDS encryption of the password.
-d Force CRY encryption of the password (default).
-p Do not encrypt the password (plaintext).
-s Force SHA encryption of the password.
-b Use the password from the command line rather than prompting for it.
On Windows, TPF and NetWare systems the '-p' flag is used by default.
All other systems, the '-p' flag will probably not work.
```

As you can see, isn't a very difficult command to use. For example, to create a new user file gniluxers with a user named wsb, you need do something like this:

```
# htpasswd -c gniluxers wsb
```

You would be prompted for a password for the user. To add more users, you would repeat the same procedure, only omitting the -c flag.

You can also create user groups. The format of these files is similar to that of /etc/groups. On each line, the group name, followed by a colon, and then list all users, with each user separated by spaces. For example, an entry in a user group file might look like this:

```
gniluxers: wsb pgj ppj aj nadia rkr hak
```