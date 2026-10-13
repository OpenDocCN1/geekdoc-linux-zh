
```
# Make sure that each exists.
cut -d: -f1,6 /etc/passwd | sed 's/:/ /g' | \
(while read acct homedir
do
  # echo checking home directory $homedir
  if [ ! -d $homedir ] ; then
    echo Warning: home directory $homedir for account $acct is missing
  fi
done )
exit 0
```

Although this might look considerably different from the previous version, a closer glance will confirm that the only significant refinement to this version of the script is that we're using surrounding parentheses around the test and output. The parentheses spawn a subshell that then has the output of the cut | sed command as its standard input, so we can use the built-in read shell command.

```
$ sh checkhomes.sh
Warning: home directory /var/adm for account adm is missing
Warning: home directory /var/spool/news for account news is missing
Warning: home directory /var/spool/uucp for account uucp is missing
Warning: home directory /var/gopher for account gopher is missing
Warning: home directory /home/root for account taylor su is missing
```

The output is definitely more user friendly!

![](img/5ced0c78d748bd190e9027e5549a3622_105_0.png)

> > Solaris has a very nifty utility pwck that does a number of these /etc/passwd consistency checks. It's well worth knowing.

5. An equally important test is whether there's more than one UID 0 (root) account, and whether there are any accounts without a password. The first test can be done with a very simple awk invocation:

```
$ awk -F: '$3 == 0 { print $0 }' /etc/passwd
root:x:0:0:root:/root:/bin/bash
```

The $3 == 0 is a conditional test: If it is true, then the entire line is printed.

![](img/5ced0c78d748bd190e9027e5549a3622_105_1.png)

> > If you ever have a change in the number of accounts with UID 0, it's time to IMMEDIATELY investigate. Remember, anyone with UID 0 access can do anything they want, including replacing login with their own version that

> e-mails account/password pairs to an e-mail address surreptitiously, or worse!

The test to see whether there are any accounts without passwords is a bit more tricky, because we need to check not only the /etc/passwd file, but also the /etc/shadow file. The trick is that only root can access the /etc/shadow file in the first place, so this command will have to be run by root:

```
# cat /etc/passwd /etc/shadow | awk -F: 'length($2) < 1 { print $0 }'
#
```

No output. Phew! What a relief!

To make this more interesting, however, I'll create a new account and omit the password:

```
# cp /etc/passwd /etc/passwd.save
# echo "taylorsu::0:502:Dave as Superuser:/home/root:/bin/bash" >> ~/etc/passwd
```

![](img/5ced0c78d748bd190e9027e5549a3622_106_0.png)

> The >> is a very dangerous command, so either don't do it at all, or do it very, very carefully. If you were to accidentally use > instead of >>, for example, you'd have just deleted your entire /etc/passwd file, which could have catastrophic results! That's why you can see that I'm also saving a copy of the /etc/passwd file as /etc/passwd.save, just in case....

Now running the zero-password test is more interesting:

```
# cat /etc/passwd /etc/shadow | awk -F: 'length($2) < 1 { print $0 }'
taylorsu::0:502:Dave as Superuser:/home/root:/bin/bash
```

Got it! How about checking for more than one UID 0 account?

```
# awk -F: '$3 == 0 { print $0 }' /etc/passwd
root:x:0:0:root:/bin/bash
taylorsu::0:502:Dave as Superuser:/home/root:/bin/bash
```

Good. That flagged it, too. To fix it, I'll use passwd to set the password for this account, and we're done with this task.

There are a number of ways that the /etc/passwd file can be analyzed and tested in an automated fashion, as we've seen in this first task. The most important thing isn't to come up with super-fancy analysis tools, but to do some sort of analysis frequently. If someone hacks into your system, they're not going to wave a flag or send you an e-mail message, so your vigilance with the accounts in the /etc/passwd file is critical!

## Password Files in BSD/Mac OS X

Darwin has a completely different approach to managing user accounts. For single-user mode, the standby /etc/passwd is available, but in normal multiuser mode, the system uses a considerably more sophisticated (and very complex) system called NetInfo.

## Task 5.2: Accounts and the Password File in Darwin

In addition to the standard Unix /etc/passwd file, BSD also works with a system called NetInfo, which has both an attractive graphical interface and a crude but powerful command-line interface available.

- 1. A simple glance at /etc/passwd shows just how different things are. Notice that I'm logged in as taylor, but that my account information doesn't even show up here!

```
$ who am i
 taylor tty1 Jan 9 12:29
$ cat /etc/passwd
##
# User Database
#
# Note that this file is consulted when the system is running in single-
# mode. At other times this information is handled by lookupd. By
# default,
# lookupd gets information from NetInfo, so this file will not be consulted
# unless you have changed lookupd's configuration.
##
nobody:*:-2:-2:Unprivileged User:/nonexistent:/noshell
root:*:0:0:System Administrator:/var/root:/bin/csh
daemon:*:1:1:System Services:/var/root:/noshell
www:*:70:70:World Wide Web Server:/Library/WebServer:/noshell
unknown:*:99:99:Unknown User:/nonexistent:/noshell
```

As the comment indicates, most user account information is stored in the cryptic NetInfo database, and can most easily be accessed from the graphical NetInfo application within the world of Mac OS X.

- 2. There are a number of different command line utilities for NetInfo too, fortunately:

```
$ man -k netinfo
netinfo(3) - library routines for NetInfo calls
netinfo(5) - network administrative information
netinfod(8) - NetInfo daemon
nibindd(8) - NetInfo binder
nicl(1) - NetInfo command line utility
nidomain(8) - NetInfo domain utility
nidump(8) - extract text or flat-file-format data from NetInfo
nifind(1) - find a directory in the NetInfo hierarchy
```

- nigrep(1) - search for a regular expression in the NetInfo hierarchy
- niload(8) - load text or flat-file-format data into NetInfo
- nireport(1) - print tables from the NetInfo hierarchy
- niutil(1) - NetInfo utility

To see the full NetInfo database, the proper command is nidump:

```
$ nidump passwd .
 nobody:*:2::0:0:Unprivileged User:/dev/null:/dev/null
 root:cBbkMtkWlh2:0:0:0:System Administrator:/var/root:/bin/tcsh
 daemon:*:1::0:0:System Services:/var/root:/dev/null
 unknown:*:99:99:0:Unknown User:/dev/null:/dev/null
 www:*:70:70:0:World Wide Web Server:/Library/WebServer:/dev/null
 taylor:fse2juv3k6jIE:501:20::Dave Taylor:/Users/taylor:/bin/tcsh
```

You can see that it's similar to the /etc/passwd file, with the exception of the taylor account. A closer look will reveal that there are more information fields listed than are in /etc/passwd.

![](img/5ced0c78d748bd190e9027e5549a3622_108_0.png)

> Note that nidump is a user-level command, and that it shows encrypted password strings rather than just a placeholder, while hiding the actual encrypted password in a shadow file. A potential security consideration, if you're paranoid about guest users!

- 3. The nidump command lists all the entries in the /etc/passwd file along with all the additional accounts set up in the NetInfo database, so modifying the earlier tests and scripts isn't too difficult. Every time we simply had "/etc/passwd" referenced, we'll instead need to stream in the output of nidump, and we'll have to modify the field count to compensate for the additional information output:

```
# nidump passwd . | cut -d: -f10 | sort | uniq -c | sort -rn
 4 /dev/null
 3 /bin/tcsh
```

However, there's a much more sophisticated way to work with NetInfo: the nireport command. This way of accessing the NetInfo information requires that you know the names of the fields in the users area of the NetInfo database. They are summarized in Table 5.1.

## TABLE 5.1 NetInfo /users Property Names

| Property Name | Explanation |
|---|---|
| name | The login name of the user |
| passwd | The encrypted password of the user |
