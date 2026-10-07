> **WARNING**

Make sure you type the password slowly and carefully. If any other user's password is lost or forgotten, it can be reset by the root login. But, if the root password is lost or forgotten, you must reinstall Linux.

Because it's so important that passwords are entered correctly, the system double-checks the spelling of the password for you by asking you to type it again:

```
Retype new password:
```

Again, what you type is not displayed on the screen. If your two password entries match, you see the following:

```
Password changed.
darkstar:~#
```

The password is now changed in the system's configuration files. The change is effective immediately, and your old password is discarded.

If the two password entries you typed do not match completely (remember, case is important), Linux gives you a message similar to this one:

```
You misspelled it. Password not changed.
```

and changes are not made to the password. You need to start over with the passwd command from the beginning.

> **TIP**

If you want to leave a program right away and return to the shell prompt, try Ctrl+C (hold the Ctrl key and press C; this is sometimes written as ^C). This usually terminates whatever program you're in (usually without ill effects) and redisplay the shell prompt. For example, if you're starting to change your password and haven't thought of a good one, pressing Ctrl+C when Linux is asking for your new password terminates the routine and your old password is kept.

# ## Creating a New Login

Now that you have assigned a password for the root account, the next step is to create a login with which you can safely explore the Linux system and try out some of the basic commands covered in the following chapters. Some Linux systems ask you to create a