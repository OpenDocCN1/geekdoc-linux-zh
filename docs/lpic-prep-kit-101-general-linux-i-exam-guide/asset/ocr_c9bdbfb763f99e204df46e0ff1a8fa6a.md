# The passwd File

All information about user accounts is included in the file /etc/passwd in a specific format. For the exam, you need to know what each field is used for and how other programs use this information. This file contains the user’s login name, user ID, password, full name, and other information as shown in Table 7.1.

| Field | Contents |
| --- | --- |
| username | Must uniquely identify the user |
| password | User’s encrypted password |
| user ID (UID) | Unique number that the operating system uses to identify the user |
| group ID (GID) | Unique number that identifies the user’s group |
| comment | User’s full name, phone number, location, or other information |
| user’s home directory | Directory in which the user is placed when she logs on |
| login command | Command that is executed upon logon, usually a shell |


Chapter 9 discusses how the permissions are set on the /etc/passwd file. This file is owned by root with root having rw\_- permissions. Everyone else, including the group, can only read this file.

A sample /etc/passwd file might look like this:

```
root::Mrczx.k5gtYoQ:0:0:root:/root:/bin/bash
hadden:44c5UQw27L6Js:500:500:Theresa Hadden,Home Office,555-5555,222-2222:/home/hadden:/bin/bash
bin:::1:1:bin:/bin:
daemon:::2:2:daemon:/sbin:
admn:::3:4:adm:/var/adm:
lp:::4:7:lp:/var/spool/lpd:
sync:::5:0:sync:/sbin:/bin/sync
shutdown:::6:0:shutdown:/sbin:/sbin/shutdown
halt:::7:0:halt:/sbin:/sbin/halt
mail:::8:12:mail:/var/spool/mail:
news:::9:13:news:/var/spool/news:
uucp:::10:14:uucp:/var/spool/uucp:
operator:::11:0:operator:/root:
games:::12:100:games:/usr/games:
gopher:::13:30:gopher:/usr/lib/gopher-data:
ftp:::14:50:FTP User:/home/ftp:
nobody:::99:99:Nobody:/:

```