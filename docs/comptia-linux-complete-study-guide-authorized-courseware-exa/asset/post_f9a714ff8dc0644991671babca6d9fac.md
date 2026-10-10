
## EXERCISE 7.1 (continued)

3. Acquire root privileges. You can do this by typing **su** in an xterm, by selecting Session > New Root Console from a Konsole, or by using **sudo** (if it's configured) to run the commands in the following steps.
4. Type **useradd -m username**, where *username* is the name you want to be associated with the account. This command creates an account. The -m parameter tells Linux to create a home directory for the user and fill it with default account configuration files.
5. Type **passwd username**. You'll be asked to enter a password for the user and to type it a second time. Enter a random string or select a password as described in "Setting a Password."
6. Press Ctrl+Alt+F2 to go to a fresh text-mode login screen. (If you're already using multiple virtual terminals, you may need to use a function key number greater than F2.)
7. Try logging in as the new user to verify that the account works properly.

In practice, creating accounts on a production system may require variations on this procedure. You may need to use additional options in step 4, for instance; consult the section “Adding Users” or the useradd man page for details on these options. Furthermore, setting the *password* may require changes. On a small system with few users, you may be able to create accounts in the presence of their future users, in which case the user can type the password in step 5. On other systems, you may need to generate *passwords* yourself and then give them to users in some way.

## Using usermod

The *usermod* program closely parallels *useradd* in its features and parameters. This utility changes an existing account instead of creating a new one, though. The major differences between *useradd* and *usermod* are as follows:

- *usermod* allows the addition of a -m parameter when used with -d. The -d parameter alone changes the user's home directory, but it doesn't move any files. Adding -m causes *usermod* to move the user's files to the new location.
- *usermod* supports a -l parameter, which changes the user's login name to the specified value. For instance, typing **usermod sally -l sjones** changes the username from *sally* to *sjones*.
- You may lock and unlock a user's password with the -L and -U options, respectively. These options duplicate functionality provided by *passwd*.

The *usermod* program changes the contents of */etc/passwd* or */etc/shadow*, depending on the option used. If -m is used, *usermod* also moves the user's files, as already noted.

## Managing Users and Groups

![](img/f339a9f48c4b443e61c74acb4c9c3da4_398_0.png)

Changing an account's characteristics while the owner is logged in can have undesirable consequences. This is particularly true of the `-d -m` combination, which can cause the files a user is working on to move. Most other changes, such as changes to the account's default shell, don't take effect until the user has logged out and back in again.

If you change the account's UID, this action does *not* change the UIDs stored with a user's files. Because of this, the user may lose access to those files. You can manually update the UIDs on all files by using the `chown` command, as described in Chapter 4. Specifically, a command like the following, issued after changing the UID on the account `sally`, restores proper ownership on the files in `sally`'s home directory:

```
# chown -R sally /home/sally
```

This action does *not* change the ownership of files that aren't in `sally`'s home directory. If you believe such files exist, you may need to track them down with the `find` command, as you'll see in the upcoming section "Deleting Accounts." Also, this command blindly changes ownership of *all* files in the `/home/sally` directory. This is probably OK, but it's conceivable that some files in that directory *should* be owned by somebody else—say, because `sally` and another user are collaborating on a project.

When using the `-G` option to add a user to new groups, be aware that any groups *not* listed will be removed. The `gpasswd` command, described in the upcoming section “Using `gpasswd`,” provides a way to add a user to one or more specific groups without affecting existing group memberships, and so it's generally preferable for this purpose.

## Using chage

The `chage` command allows you to modify account settings relating to account expiration. It's possible to configure Linux accounts so that they automatically expire if either of two conditions is true:

- The password hasn't been changed in a specified period of time.
- The system date is past a predetermined time.

These settings are controlled through the `chage` utility, which has the following syntax:

```
chage [-l] [-m mindays] [-M maxdays] [-d lastday]  [-I inactivedays]
[-E expiredate] [-W warndays] username
```

The program's parameters modify the command's actions:

**Display information** The `-l` option causes `chage` to display account expiration and password aging information for a particular user.

**Set the minimum time between password changes** The `-m mindays` parameter sets the minimum number of days between password changes. 0 indicates that a user can change a password multiple times in a day; 1 means that a user can change a password once a day; 2 means that a user may change a password once every two days; and so on.

**Set the maximum time between password changes** The `-M maxdays` parameter sets the maximum number of days that may pass between password changes. For instance, 30 requires a password change approximately once a month.

![](img/f339a9f48c4b443e61c74acb4c9c3da4_399_0.png)

> If the user changes a password before the deadline, the counter is reset from the password-change date.

**Set the last password change date** The `-d lastday` parameter sets the last day a password was changed. This value is normally maintained automatically by Linux, but you can use this parameter to artificially alter the password change count. *lastday* is expressed in the format *YYYY*/MM/DD or as the number of days since January 1, 1970.

**Set the maximum inactive days** The `-I inactivedays` parameter sets the number of days between password expiration and account disablement. An expired account may not be used or may force the user to change the password immediately upon logging in, depending on the distribution. A disabled account is completely disabled.

**Set the expiration date** You can set an absolute expiration date with the `-E expiredate` option. For instance, you might use `-E 2010/05/21` to have an account expire on May 21, 2010. The date may also be expressed as the number of days since January 1, 1970. A value of -1 represents no expiration date.

**Set the number of warning days** The `-W warndays` option sets the number of days before account expiration that the system will warn the user of the impending expiration. It's generally a good idea to use this feature to alert users of their status, particularly if you make heavy use of password-change expirations. Note that these warnings are usually only shown to text-mode login users; GUI login users, file-share users, and so on usually don't see these messages.

The `chage` command can normally be used only by root. The one exception to this rule is if the `-l` option is used; this feature allows ordinary users to check their account-expiration information.

## Directly Modifying Account Configuration Files

User configuration files can be modified directly. /etc/passwd and /etc/shadow files control most aspects of an account's basic features. Both files consist of a set of lines, one line per account. Each line begins with a username and continues with a set of fields, delimited by colons (:). Many of these items may be modified with usermod or passwd. A typical /etc/passwd entry resembles the following:

```
sally:x:529:100:Sally Jones:/home/sally:/bin/bash
```

Each field has a specific meaning, as follows:

**Username** The first field in each /etc/passwd line is the username (sally in this example).
