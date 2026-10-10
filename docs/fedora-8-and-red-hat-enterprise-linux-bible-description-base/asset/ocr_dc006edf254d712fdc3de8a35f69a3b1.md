Each line in this listing corresponds to a single user account on the Linux system. Each line is made up of seven fields separated by colon (:) characters. From left to right the fields are the login name, the encrypted password, the user ID, the group ID, the description (usually a person's name), the home directory, and the default shell. Looking at the first line, you see that it is for the root account and has an encrypted password of DdkS6lUke79flQ. You can also see that root has a user ID of zero, a group ID of zero, and a home directory of /root, and root's default shell is /bin/sh.

All of these values are quite normal for a root account, but seeing that encrypted password should set off alarm bells in your head. It confirms that your system is not using the shadow password file. At this point, you should immediately convert your password file so that it uses /etc/shadow to store the password information. You do this by using the pwconv command. Simply log in as root (or use the su command to become root) and enter the pwconv command at a prompt. It will print no messages, but when your shell prompt returns, you should have a /etc/shadow file and your /etc/passwd file should now look like this:

```
root::x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
.
.
.
mary:x:500:100:Mary Smith:/home/mary:/bin/sh
joe::x:501:100:Joe Johanson:/home/joe:/bin/sh
jane::x:502:100:Jane Anderson:/home/jane:/bin/sh
bob:x:503:100:Bob Renolds:/home/bob:/bin/sh
```

Encrypted password data is replaced with an x. Password data has been moved to /etc/shadow.

To check the type of password authentication your system is using, open the Authentication window (System \rightarrow Administration \rightarrow Authentication from the GNOME desktop). This tool lets you choose to use MD5 passwords, LDAP authentication, Kerberos 5, or other authentication methods.

To work with passwords for groups, you can use the grppconv command to convert passwords in /etc/groups to shadowed group passwords in /etc/gshadow. If you change passwd or group passwords and something breaks (you are unable to log in to the accounts), you can use the pwconv and grpconv commands, respectively, to reverse password conversion.

So, now you are using the shadow password file and picking good passwords. You have made a great start toward securing your system. You may also have noticed by now that security is not just a one-time job. It is an ongoing process, as much about policies as programs. Keep reading to learn more.