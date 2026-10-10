**13.4** Whoever is in group disk has block-level read and write permission to the system's disks. With knowledge of the file system structure it is easy to make a copy of /bin/sh into a SUID root shell (Section 14.4) by changing the file system metadata directly on disk. Thus, group disk membership is tantamount to root privileges; you should put nobody into the disk group whom you would not want to tell the *root* password outright.

**13.5** You will usually find an “x”. This is a hint that the password that would usually be stored there is indeed stored in another file, namely */etc/shadow*, which unlike the former file is readable only for root.

**13.6** There are basically two possibilities:

+   1. Nothing. In this case the system should turn you away after you entered your password, since no user account corresponds to the all-uppercase user name.

+   2. From now on, the system talks to you in uppercase letters only. In this case your Linux system assumes that you are sitting in front of an absolutely antediluvian terminal (1970s vintage or so) that does not support lowercase letters, and kindly switches its processing of input and output data such that uppercase letters in the input are interpreted as lowercase, and lowercase letters in the output are displayed as uppercase. Today this is of limited benefit (except if you work in a computer museum), and you should log out as quickly again as possible before your head explodes. Since this behaviour is so atavistic, not every Linux distribution goes along with it, though.

**13.7** Use the *passwd* command if you're logged in as user *joe*, or “*passwd* *joe*” as *root*. In *joe*'s entry in the */etc/shadow* file there should be a different value in the second field, and the date of the last password change (field 3) should show the current date (in what unit?)

**13.8** As *root*, you set a new password for him using “*passwd dumbo*”, as you cannot retrieve his old one even though you are the administrator.

**13.9** Use the command “*passwd* -n 7 -m 14 -w 2 *joe*”. You can verify the settings using “*passwd* -S *joe*”.

**13.10** Use the *useradd* command to create the user, “*usermod* -u*” to modify the UID. Instead of a user name, the files should display a UID as their owner, since no user name is known for that UID ...

**13.11** For each of the three user accounts there should be one line in */etc/passwd* and one in */etc/shadow*. To work with the accounts, you do not necessarily need a password (you can use *su* as *root*), but if you want to login you do. You can create a file without a home directory by placing it in */tmp* (in case you forgot—a home directory for a new user would however be a good thing).

**13.12** Use the *userdel* command to delete the account. To remove the files, use the “*find* / -UID *(UID)* *-delete*” command.

**13.13** If you use “*usermod* -u*”, you must reassign the user's file to the new UID, for example by means of “*find* / -uid *(UID)* *-exec chown* *test1 {} ;*” or (more efficiently) “*chown* -R --from=*(UID)* *test1* /”. In each case, *(UID)* is the (numerical) former UID.

**13.14** You can either edit /etc/passwd using *vi*" or else call *usermod*.