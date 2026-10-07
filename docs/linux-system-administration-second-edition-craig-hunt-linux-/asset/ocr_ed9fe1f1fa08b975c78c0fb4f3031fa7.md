# ## The /etc/passwd File

Information about each user is contained in the /etc/passwd file. As a system administrator, it is critical that you clearly understand this important file. In the excerpt shown in Listing 5.1, you'll notice that root is listed first. The root user is always assigned the user ID (UID) 0 and group ID (GID) 0. Other special users and accounts associated with services and daemons are listed after root and always have UID and GID values below 100; Red Hat starts UIDs at 500 just to be safe. Last, regular, and special accounts for individual users are listed.

# ### Listing 5.1: An Example of an /etc/passwd File

```
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:
daemon:x:2:2:daemon:/sbin:
adm:x:3:4:adm:/var/adm:
lp:x:4:7:lp:/var/spool/lpd:
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:
news:x:9:13:news:/var/spool/news:
uucp:x:10:14:uucp:/var/spool/uucp:
operator:x:11:0:operator:/root:
games:x:12:100:games:/usr/games:
gopher:x:13:30:gopher:/usr/lib/gopher-data:
ftp:x:14:50:FTP User:/home/ftp:
nobody:x:99:99:Nobody:/:
xfs:x:43:43:X Font Server:/etc/X11/fs:/bin/false
named:x:25:25:Named:/var/named:/bin/false
marty:x:500:500:Not Feldman:/home/marty:/bin/bash
ermie:x:501:501:Earnest too:/home/ermie:/bin/csh
betty:x:502:502:Ready Betty:/home/betty:/bin/pop
donald:x:503:503:Unka Donald:/home/donald:/bin/bash
```

Looking at the last entry, Donald's record, you can see the following column-delimited fields:

+   * **Username** Donald's username is not capitalized. Typically, initial capitalization is not used in order to avoid upper/lowercase confusion. There is no default value for the username field.

+   * **Encrypted Password** Technically, this field holds the password for users; however, this particular Linux system is using *shadow passwords*, which are held in /etc/shadow. Therefore the /etc/passwd file contains an x in the second field to indicate to login that the actual password is held elsewhere. Shadow passwords are discussed more fully later in this chapter.

+   * **User ID** Throughout the system, any file owned or created by Donald will have this number associated with it. It is actually this UID that will be associated with Donald's files, and the human-friendly donald is what is displayed to us, for example by the ls command. Also, every process executing on the system will be associated with a UID. Typically it's the UID of the user who starts up the process.

+   * **Default GID** This is Donald's login group. All files are owned by both a user and a group. When Donald creates a new file, it will by default receive his GID value, which will also be associated with the file. It is no coincidence that Donald has a GID equal