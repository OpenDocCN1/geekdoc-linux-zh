+   • Select only those package groups that you need for your system when installing Red Hat Linux. Do not install any unnecessary software. For example, if your system is a workstation, you do not need to install most of the server packages, such as the Web server, news server, e-mail server, and so on.

+   • Create initial user accounts and make sure that all passwords are strong ones that password-cracking programs cannot guess. As you will learn in the next section, “Securing Passwords,” Red Hat Linux includes the tools to enforce strong passwords.

+   • Enable only those Internet services that you need on a system. In particular, do not enable services that are not properly configured. Later in this session, in the section titled “Securing Internet Services,” you learn about enabling and disabling Internet services.

+   • Check various log files periodically for signs of any break-ins or attempted break-ins. These log files are in the /var/log directory of your system.

+   • Check security news by regularly visiting and installing updates from Red Hat once a fix becomes available.

# Securing passwords

Historically, UNIX passwords were stored in the /etc/passwd file, which any user could read. For example, a typical old-style /etc/passwd file entry for the root user looks like this:

```
root:t6T7NWDLK1K8u:0:0:root:/root:/bin/bash
```

The fields are separated by colons (:) and the second field contains the password in encrypted form. To check if a password is valid, the login program encrypts the plain-text password entered by the user and compares it with the contents of the /etc/passwd file. If there is a match, the user is allowed to log in.

Password-cracking programs work just like the login program except that these programs pick one word at a time from a dictionary, encrypt the word, and compare the encrypted word with the encrypted passwords in the /etc/passwd file for a match. To crack the password, the intruder needs the /etc/passwd file. Often, crackers use weaknesses of various Internet servers (such as mail and FTP) to get a copy of the /etc/passwd file.

Recently, several improvements have been made to UNIX passwords to make them more secure. These include shadow passwords and pluggable authentication modules, described in the next two sections.

![](bbox=[0.06, 0.9, 0.95, 0.98])