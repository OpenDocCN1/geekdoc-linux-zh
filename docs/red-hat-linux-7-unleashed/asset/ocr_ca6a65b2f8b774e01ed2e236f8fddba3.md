In order to use Basic authentication you will need a file that lists which users are allowed to access the resources. This list will consist of a plain text file containing name and password pairs. It looks very much like the user file of your Linux system—that is, `/etc/passwd`. In fact, you could actually use this as a user list for authentication. But this is a very bad idea!

![](bbox=[0.08, 0.23, 0.35, 0.26])

> When you are using Basic authentication, passwords and usernames are sent as base64-encoded text from the client to the server—which is just as readable as plain text. The username and password are included in each request that is sent to the server. So anyone who might be snooping on Net traffic could be able to get hold of this information!

To create a user file for Apache, use the `htpasswd` command. This is included with the Apache package and if you installed using the RPMs it will be found in `/usr/bin`. Running `htpasswd` without any options will produce the following output: `Usage:` `htpasswd [-cmdps] passwordfile username` `htpasswd -b[cmdps] passwordfile username password`

+   - -c Create a new file.
+   - -m Force MD5 encryption of the password.
+   - -d Force CRYPT encryption of the password (default).
+   - -p Do not encrypt the password (plaintext).
+   - -s Force SHA encryption of the password.
+   - -b Use the password from the command line rather than prompting for it. On Windows and TPF systems the `-m` flag is used by default. On all other systems, the `-p` flag will probably not work.

As you can see, it is not a very difficult command to use. For example, to create a new user file named `gnulixusers` with a user named `wsb` you would need to do something like this: `htpasswd -c gnulixusers wsb`

You would then be prompted for a password for the user. To add more users you would repeat the same procedure, only omitting the `-c` flag.

You can also create user group files. The format of these files is more or less like the `/etc/groups`. The first entry on a line is the group name. A colon follows this and then a list of all users is specified, separated by spaces. For example, an entry might look like this: `gnulickers: wsb pgy jp ajje nadia rkr hak`