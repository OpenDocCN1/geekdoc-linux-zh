```
```
$ who
sam   tty4  2010-07-25 17:18
max   tty2  2010-07-25 16:42
zach  tty1  2010-07-25 16:39
max   pts/4 2010-07-25 17:27 (coffee)
```
```

Figure 5-10 who lists who is logged in

The information that who displays is useful when you want to communicate with a user on the local system. When the user is logged in, you can use write (page 184) to establish communication immediately. If who does not list the user or if you do not need to communicate immediately, you can send email to that person (page 185).

If the output of who scrolls off the screen, you can redirect the output through a pipe (|, page 170) so that it becomes the input to less, which displays the output one screen at a time. You can also use a pipe to redirect the output through grep to look for a specific name.

If you need to find out which terminal you are using or what time you logged in, you can use the command who am i:

```
```
$ who am i
max   tty2  2010-07-25 16:42
```
```

# finger: Lists Users on the System

You can use finger to display a list of users who are logged in on the local system. In addition to usernames, finger supplies each user’s full name along with information about which device the user’s terminal is connected to, how recently the user typed something on the keyboard, when the user logged in, and what contact information is available. If the user has logged in over the network, the name of the remote system is shown as the user’s location. For example, in Figure 5-11 Max is logged in from the remote system named coffee. The asterisks (\*) in front of the device names in the Tty column indicate that the user has blocked messages sent directly to his terminal (refer to “mesg: Denies or Accepts Messages” on page 185).

```
```
$ finger
Login      Name          Tty     Idle  Login Time   Office ...
sam        Sam the Great *tty4         29  Jul 25 17:18
zach       Zach Brill    *tty1   1:07  Jul 25 16:39
max        Max Wild      *tty2         3   Jul 25 17:27 (coffee)
```
```

Figure 5-11 finger | lists who is logged in