System user accounts aren't used for login. Instead, they are used by services running on the system. When one of these services needs to do something in the Linux file system, it does so as its associated user account from /etc/passwd. Notice that the system user accounts have a much lower UID number as compared to standard user accounts. UIDs between 0 and 499 are typically reserved for system accounts, depending on the distribution.

For example, suppose I've logged in to the ftp service on my Linux system as an anonymous user and uploaded a file. This file needs to be written to the ftp service's default directory in the file system. When it writes, it does so as the ftp user. By doing this, we can use permissions (discussed later in the chapter) to control what a given service can or can't do.

Let's next look at the /etc/shadow file.

# The /etc/shadow File

With most Linux distributions that use local authentication, user passwords are stored in encrypted format in the /etc/shadow file. This file is linked to the /etc/passwd file we discussed previously. Each of the user accounts listed in /etc/passwd has a corresponding entry in /etc/shadow, as shown in this example:

```
```
ws1:~ # cat /etc/shadow
...
root:$2a$05$9hO3HEGGFS12l8G1oToYGyreBe1OHLHc:/:2/KxyQGF7RS0:/TdLOrdDja:15035::::::
ssh:!!:14796::0:99999:7:::
uucp:*:14796::::::
wwwrun:*:14796:::
ksanders:$2a$05$85KKL1DbTbqSEMI1.2FoI3ue4bdYr.el6GMKs7MU6.n2I5SCC7/
REUS:15043::0::99999:7:::
taxu:$2a$05$4550SUO1Ol8JewMlPV5881exLKa4MD9p3T25VePcICdieiHxVp.yJhw-
pc:15041::0::99999:7:::
```
```

As with /etc/passwd, each user account is represented by a single line in the /etc/shadow file. Each record is composed of the following fields, each separated by a colon:

```
```
Username:Password:Last_Modified:Min_Days:Max_Days:Days_Warn:Disabled_Days:Expire
```
```

For example, the record for ksanders is as follows:

```
```
ksanders:$2a$05$85KKL1DbTbqSEMI1.2FoI3ue4bdYr.el6GMKs7MU6.n2I5SCC7/
REUS:15043::0::99999:7:::
```
```

Here's what each of these fields contains:

+   - **Username** This is the user's login name from /etc/passwd.
+   - **Password** This is the user's password in encrypted format. In the preceding example, the password for ksanders is M3linux273. However, to prevent someone from accessing the /etc/shadow file and grabbing your user passwords from it, it is stored in encrypted format. You may notice that all of the system user accounts have a simple asterisk in this field (*). This indicates that these accounts aren't allowed to log in to the system. For example, if I