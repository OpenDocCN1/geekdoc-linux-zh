terminal so that another user on the same system can use the write command to write text messages to you:

```
mesg y
```

The n option allows you to disable write access. If you do not wish to be bothered by anyone at any time, you can add mesg n to your login script (.login) file in your home directory.

# write

Syntax: write username tty

This program allows you to write text messages to the named user if he or she has not disabled write access to her tty. For example:

```
write shoeman
```

This command allows you to type a text message on screen, and when you finish the message by pressing Ctrl+D, the message is displayed on the user shoeman's terminal. If the user is logged in more than once, you have to specify the terminal name as well. For example:

```
write shoeman ttyp0
```

This allows you to write to shoeman and to display the message on terminal ttyp0. If someone has multiple terminals open, you might want to run the w or who command to see which tty is most suitable.

# Shell Commands

In this section, you will find some very basic shell commands. These commands allow you to create alias names for other commands, recall commands that you have executed earlier in the current session, set and view environment information, and so on.

# alias

Syntax: alias name of the alias = command