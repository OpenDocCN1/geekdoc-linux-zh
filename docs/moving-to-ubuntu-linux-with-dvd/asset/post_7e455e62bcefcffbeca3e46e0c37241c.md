
## Give Me More!

For those of you who get to the end of the chapters in this book and find yourselves wanting to know *more* about the shell, check out Appendix A.

Here’s our polite introduction. Click the Terminal menu item and a rather empty window appears. Along the top is a menu bar with some quick access items arranged according to how they affect the terminal session. Below that, in the larger part of the window, you see a flashing cursor sitting beside a dollar sign prompt. This is the shell prompt. Whenever you find yourself at a shell prompt, the system is waiting for you to type in a command. Remember the calculator example from earlier? You could type `gcalctool` here and have it start up just as easily. For now, type `date` at the shell prompt, and press the <Enter> key (see Figure 3-12).

![](img/0e9cf4c65a042f4a9bea644dc50153a7_77_0.png)

Now that you know the date and time that I wrote this paragraph, when you try it, you’ll get your current date and time. That’s what date is: a command that displays the date and time. You’ll also find yourself back at the shell prompt as your system patiently awaits your next command. Type **exit** and press the <Enter> key.

The terminal program disappears. That's it. We'll use the shell again as we go through this book, but for now, your polite introduction to the shell ends here.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_78_0.png)

> ### Funny Tip
> Be careful not to type `ddate` instead of `date`. You will wind up with the Discordian Date, a numbering system from the Church of the Subgenius. For instance:
>
> $ ddate
>
> Today is Sweektmorn, the 46th day of Chaos in the YOLD 3172

## Changing Your Password; It's All About You!

It is good security policy to change your password from time to time. Look along the top panel and click **System**, **Preferences**. Right at the top, you should see an entry labeled **About Me**. A personal information window appears, from which you can change or fill in a great deal of personal information (see Figure 3-13). You can also run the command as in the calculator example above by using your <Alt+F2> run sequence and typing the command `gnome-about-me`.

You might be asking why Ubuntu provides a space for all these details about you. You don't have to fill in any information here, but several applications do look here. For instance, in Chapter 11, I'll tell you all about the **Evolution** email package and its contact Management functions. In your Evolution address book, there's an entry created for you, which you can send as a virtual business card. The real point of this exercise, however, is to change your password. Click the **Change Password** button in the top right corner. Doing so brings up the **Change Password** dialog shown in Figure 3-14.

Notice that, like the login manager, your password is not visible. Instead, each key you press is echoed as an asterisk. When you have successfully entered your password, the system asks you for a new password. Then, you are asked for the password again, for confirmation. That's it. Be sure to remember your new password. You'll need it the next time you log in.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_79_0.png)

Figure 3–13 The About Me dialog provides quick access to your personal information. It also happens to be a way to change your password.

### Shell Out

You can easily change your password from the command line as well. Just open a shell prompt and type the command:

```
[marcel@mySystem marcel]$ passwd
Changing password for user marcel.
Changing password for marcel
(current) UNIX password:
New UNIX password:
Retype new UNIX password:
passwd: all authentication tokens updated successfully.
```

Although the steps are essentially the same, the wording of the actual password change dialog can change from system to system.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_80_0.png)

Figure 3–14 To change your password, you must type the new password twice.

Speaking of passwords . . .

## User Security

As I mentioned earlier in the book, Linux is a multiuser operating system, meaning that one or more users can work on it at the same time. This also means that each person using your system is an individual, with his or her own home directories, files, menus, and desktop decorations. By creating a login for each member of your family or office, you not only protect the files that belong to each user, but you also protect yourself. If little Natika deletes all her icons or changes the desktop to a garish green and purple, it doesn't affect you. Similarly, this is a great opportunity to create a play world for the kids.

Each user is referenced by a username. Each username has a user ID (UID) associated with it and one or more groups. Like usernames, group names are also represented by a numeric identifier, this time called a group ID (GID). A user's UID is unique, as is a group's GID.

Adding users requires that you operate as root, so when you launch the GNOME users administration tool (command name `users-admin`), you are asked for your password. When the program starts, a window appears like the one in Figure 3-15. There are two tabs, one for Users and the other for Groups.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_81_0.png)

By default, only nonadministrative user accounts are shown. With a fresh Ubuntu installation, that generally means only one user, the one you set up at install time. To see all users on the system, click the Show All Users and Groups check box at the lower left. To add a user, click the Add User button on the right. A new window, the User Account Editor, appears (see Figure 3–16).

Most of the information on this page is optional. In fact, all you need to enter is a username and a password. The other fields are provided to further identify the person for whom you are creating the login. For instance, you can choose to enter his or her full name, office location, phone number, and so on.

The most important part of this process has to do with entering the password information. By default, you have the opportunity to Set Password by Hand. The radio button for this area should already be selected. Choose a password and enter it into the User Password field. You must enter it twice, the second time in the Confirmation field. Note that when you do enter the password, you don’t actually see it, but rather stars echo your keystrokes. You can also ask the program to generate a random password by selecting the last radio button, then clicking the Generate button. When you are done, click OK.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_82_0.png)

Figure 3–16 Setting user properties.

This takes you back to the Users and Groups screen, where you can simply click OK to finish. Of course, you can also add more users.

## Much Ado About sudo

When you start a graphical command that requires administrative privileges, a dialog appears asking you for your password. This dialog is actually a command called gksudo. In turn, gksudo is a wrapper for a shell command called sudo.

For those of you who may have used other Linux (or UNIX) systems, you may have had access to an account called root. This is the superuser account with ultimate power over the system. Ubuntu locks down the root account and does not allow a direct login. To execute commands with root privileges, Ubuntu makes use of the *sudo* command.

When you run a program with sudo (or gksudo), you are asked for your password to confirm access. After entering your password, your account can execute additional root-level commands for the next 15 minutes without having to reenter your password. That said, you still need to preface your commands with *sudo* or *gksudo*.

To run a command inside a GNOME terminal session, or a command shell, preface the command with *sudo*.

```
sudo command_name
```

From time to time, you may need to run several commands with root privileges. At those times, it may get a little tiring to prefix each and every command with *sudo*. To get around this, you can enter a session with administrative privileges by typing the following.

```
sudo -i
```

When you are through with your admin session, type **exit**.

In Chapter 21, I give an extended tour of the command shell. There, you will have additional opportunity to see *sudo* in action.

![](img/0e9cf4c65a042f4a9bea644dc50153a7_83_0.png)

> *Note* Always use **gksudo** when running graphical applications that need administrative privileges.

## I Need More Help!

Way back in the introduction to the book, I gave you a list of places that you might look to for help, some online and others in the community. As it turns out, your desktop has a very handy and fairly impressive collection of help, right at your fingertips.

The GNOME documentation browser, or Help Center, if you prefer (command name *help*) is something you've probably already guessed at.
