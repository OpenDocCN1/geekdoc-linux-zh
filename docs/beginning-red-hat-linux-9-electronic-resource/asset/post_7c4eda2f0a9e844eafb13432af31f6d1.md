
Second, the tools they carry out proper **file locking**. This is a mechanism that prevents overwriting problems in a situation where several administrators try to manage users at the same time.

It is definitely convenient to be able to examine these configuration files, but when you need to make adjustments to them, it’s safest to use the designated tools – the graphical **User Manager** interface that we’ve already seen, and the command line tools that we’ll examine next.

## Some Useful Command Line Tools

If you plan to use the command line tools to manage your users and groups, then you’ll need to do so in the context of the root account. Having fired up a terminal window, there are a few clues to remind you which account you’re logged in as – remember that the typical root shell prompt is denoted with the # character, while the prompt for an ordinary user account is denoted with $ or >.

You can also use the `id` command to check your identity:

```
$ id
uid=500(eziogm) gid=500(eziogm) groups=500(eziogm),503(authors)
```

The output above shows that the user is logged in as the `eziogm` account. (Note that it also confirms information about the account’s group membership – in particular, that its primary group is also called `eziogm` and that the user is a member of two groups, `eziogm` and `authors`.)

To run in the context of the root account in a terminal window, simply execute the `su` (switch user) command at the command line:

```
$ su -
Password:
```

You’ll be prompted to type the root password, as shown above. The effect of the `su` command is to execute a new shell under a different user account. Note that the new shell doesn’t *substitute* the existing shell. Instead, the new shell runs *on top* of the existing shell. To demonstrate this point, take a look at the following screenshot, which shows a user switching from `eziogm` to root, using the root shell and then leaving it:

# Chapter 8

![](img/b852150740856958b10aff9e8c9d2adc_311_0.png)

As you can see, new (root) shell terminates (via the exit command), the terminal window remains open and reverts to the context of the original account.

Note that the su command here is accompanied by a – symbol. This ensures that the new shell is treated just like any other login shell. In particular, it means that the login scripts associated to the user account (root in this case) will be executed just as if root were logging in from a terminal. These scripts have a number of effects. For example, in this case:

- They set the current working directory to be that of root’s home directory
- They set the $PATH environment variable (the search path for executable programs) to the value associated with the root user – by adding the directories /sbin and /usr/sbin. These two directories contain administrative programs that are used only by administrative accounts.

If the – character is omitted, the su command will execute a shell but will not execute the login scripts.

> If you use su to switch to the root account, and then find that various administrative commands are “missing”, then it could be that you omitted the – switch: that is, you typed just su instead of su –.

> Note also that you can use su to execute a shell with an account other than root, for example:

```
$ su kapils
$ su – kapils
```

We’re now ready to add new users to the system using the command line.

## Adding Users at the Command Line

Adding users can be a straightforward task on a stand-alone PC, but when you’re a professional system administrator with a lot of settings to get through, the graphical User Manager tool can make the task a time-consuming one.

Hence, it sometimes makes more sense to make use of command line tools instead. Once you've got the hang of the command line tools, it's easy to include them in automated scripts, and hence perform complex or lengthy operations more quickly. As you'd expect, the command line tools also have lots of options and are rather more flexible than their GUI counterparts.

### Try It Out: Adding Users with the Command Line Interface

In its simplest form, here's the sequence of commands that replicates the behavior of the graphical tool, using default values when possible.

1.  At a *root shell* prompt, type the following command to add a new user taking all the defaults:
    ```
    # useradd -c 'Mark Mamone' -s /bin/bash markm
    ```
2.  Before proceeding, use the *gedit* text editor to examine the configuration files. First, in */etc/passwd*, you should find the following new entry, for the account you've just created:
    ```
    ...
    eziomd:x:500:500:Pancrazio 'Ezio' de Mauro:/home/eziomd:/bin/bash
    kapils:x:501:501:Kapil Sharma:/home/kapils:/bin/bash
    deepakt:x:502:502:Deepak Thomas:/home/deepak/:bin/bash
    markm:x:503:504:Mark Mamone:/home/markm:/bin/bash
    ```
    
    The UID is 503 and the primary, private GID is 504. Next, from */etc/group*, we read:
    
    ```
    ...
    eziomd:x:500:
    kapils:x:501:
    deepakt:x:502:
    authors:x:503:eziomd,kapils,deepakt
    markm:x:504:
    ```
    
    From this, we can deduce that the group with GID 504 is called *markm*. Finally, there's a new line in */etc/shadow*:
    
    ```
    ...
    eziomd:$1$W/RgbXr$I5OP9t9IyVmQyvPfxnXLUfWq1:12100:0:99999:7:::
    kapils:$1$1$68Q7C14g$CqbN8rDCBw4GmxLDlouQ2g/:12100:0:99999:7:::
    deepakt:$1$SuEjrHGF$13cSo2TRmKIbN55wELfgFB1:12100:0:99999:7:::
    markm:$!:12100:0:99999:7:::
    ```
    
    The **!!** in the second field means that the account is disabled. In fact, this is the default behavior of *useradd* – it creates disabled accounts.
3.  To enable the newly created account, we must assign a password. Still using the root account, use the passwd command to assign a password for markm:
    ```
    # passwd markm
    Changing password for user markm.
    New password: (password not shown)
    Retype new password: (password not shown)
    passwd: all authentication tokens updated successfully.
    ```
4.  Now refresh your view of the /etc/shadow, to see what has changed:
    ```
    ... 
    eziomd:$1$W/RgbXr$I5OP9t9IyVmQyvPfxnXLUfWq1:12100:0:99999:7:::
    kapils:!!$1$68Q7C14g$CqbN8rDCBw4GmxLDlouQ2g/:12100:0:99999:7:::
    deepakt:$1$SuEjrHGF$13cSo2TRmKIbN55wELfgFB1:12100:0:99999:7:::
    markm:$1$3afRSvJz$mg92zGakghspD.fcpDwx4wv0:12100:0:99999:7:::
    ```
    
    Now the markm account has a password, and is fully operative.
5.  To test out the markm account, open a new terminal window as a normal user. Then use the su command to verify that the account works:
    ```
    $ su - markm
    Password: (password not shown)
    $ id
    uid=503(markm) gid=504(markm) groups=504(markm)
    ```
    
    As you can see, the new user identity is now markm. The new current directory is /home/markm, because we used the su - form:
    ```
    $ pwd
    /home/markm
    $ ls -a
    . .. .bash_logout .bash_profile .bashrc .emacs .gtkrc
    ```

### How It Works

The useradd command creates a new user called markm. The description, Mark Mamone, is delimited by single quotation marks to instruct the shell to keep it as a single parameter. The shell is /bin/bash:

```
# useradd -c 'Mark Mamone' -s /bin/bash markm
```

The passwd command assigns a password to the account. The password is to be accepted but not displayed:

```
# passwd markm
```

Other aspects of the account are determined automatically from the system defaults and from the arguments we've specified. By default, the home directory will be /home/markm; the UID and GID will be the first available (in our case 503 and 504 respectively), and the account and password expiration data are taken from /etc/login.defs and /etc/default/useradd.

You might be surprised to find that the newly created home directory is not empty. Its content is copied from the /etc/skel directory, which contains the files and directories that should be added to a new home directory whenever a new user account is created. This is a particularly handy feature for the system administrator: if every user needs a similar setup, it is sufficient to put the desired files in /etc/skel.

Other defaults, like password-aging values, are taken from /etc/login.defs.

### More on the useradd and passwd Commands

The useradd command has several options that you can use when the defaults are not appropriate. More details are available by typing man useradd in a terminal. Here's a list of the most commonly used options:

| Option | Purpose |
|:-------|:--------|
| -d | Allows you to specify the user's home directory |
| -e | Allows you to specify the expiration date of the account in the format DD-MM-YYYY (two digits for the day, two for the month, four for the year) |
| -f | If the password expires, the operating system will wait a number of days before permanently disabling the account. This option allows you to specify the number of days between these two events |
| -g | Allows you to specify the GID of this account |
| -G | Allows you to specify a comma-separated list of other groups to which the user belongs |
| -M | Allows you to omit the creation of a home directory |
| -u | Allows you to specify the UID of this account |

The passwd command can be used whenever a password needs to be changed or initialized. Of course, normal (non-root) users are allowed to change only their own passwords – they can do this via the passwd command. Root can change anyone's password, and to do that they can specify the passwd command followed by the account name (as we saw in Step 3 of the example above).
