Notice that you can change an account’s default group and provide memberships to additional groups. Account groups are covered in detail later in this chapter.

Where **usermod** comes in really handy is in a situation where you’ve created an account but forgot to check the distribution’s account creation configuration settings. Listing 10.17 shows an example of this on an Ubuntu Desktop distribution.

# **Listing 10.17:** Using usermod to modify an account

```
$ **sudo** useradd -md /home/DBowman DBowman
$ 
$ **sudo** getent passwd DBowman
DBowman:x:1003:1003::/home/DBowman:/bin/sh
$ 
$ **sudo** usermod -s /bin/bash DBowman
$ 
$ **sudo** getent passwd DBowman
DBowman:x:1003:1003::/home/DBowman:/bin/bash
$ 
```

In Listing 10.17, the user account **DBowman** is created, but when the account record is checked using the **getent** utility, it shows that the `/bin/sh` shell is being used instead of the Bash shell. To fix this problem, the **usermod** command is employed with the `-s` option, and the account’s shell is modified to the `/bin/bash` shell instead.

# ## Deleting Accounts

Deleting an account on Linux is fairly simple. The **userdel** utility is the key tool in this task. The most common option to use is the `-r` switch. This option will delete the account’s home directory tree and any files within it. Listing 10.18 shows an example of deleting an account.

# **Listing 10.18:** Using userdel to delete an account

```
$ **sudo** ls -a /home/DBowman
. .. .bash_logout .bashrc examples.desktop .profile
$ 
$ **sudo** getent passwd DBowman
DBowman:x:1003:1003::/home/DBowman:/bin/bash
$ 
$ **sudo** userdel -r DBowman
userdel: DBowman mail spool (/var/mail/DBowman) not found
$ 
$ **sudo** ls -a /home/DBowman
ls: cannot access ‘/home/DBowman’: No such file or directory
```