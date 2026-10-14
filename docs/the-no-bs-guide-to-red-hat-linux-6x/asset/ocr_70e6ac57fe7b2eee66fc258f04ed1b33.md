But why would you want to use su when you can have multiple log-ins via virtual consoles (see Chapter 4, "Living in a Shell")? Because it's sometimes quicker or more convenient to switch between users using su, and because you may have no virtual consoles available—you may be using all of them or, if you're logged in to the machine via a modem, virtual consoles may not be available to you.

# TELL ME WHO IS LOGGED IN

If you want to know which users are currently logged in to your Linux system, which console they're using, and the date and time they logged in, issue the who command. You'll see output something like this:

```
who
root             tty1      Nov 2 17:57
hermie           tty3      Nov 2 18:43
sigmund          tty2      Nov 2 18:08
```

In the output shown here, the term tty stands for teletype. In the olden days of computing, a terminal was just a keyboard with an attached printer, so you read everything off the teletype.
If you've logged in with multiple virtual consoles and changed your identity on any of them, you may have some trouble figuring out who you are—or at least what user is logged in to the console you're using. If you find yourself in such an identity crisis, try this variant of the who command:

```
who am i
```

# WHAT'S TODAY'S DATE?

Use the date command to print the current date and time. If you add the -u flag, the results will be for the Greenwich mean time zone. And if you log in as a superuser, you can even change the date or time with the -s flag. Now, that's power! Here are some examples:

```
date                          Print the date and time
Sat Nov 2 20:09:43 EST 1996

date -u                        Print the GMT date and time
Sun Nov 3 01:09:45 GMT 1996

date -s 0503                   Set the clock to 5:03 AM
```