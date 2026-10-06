# Communicating with Other Users

$ write alex
Hi Alex, are you there? o

**Figure 3-14** The write utility I

The **destination-user** is the login name of the user you want to communicate with. The **terminal** is the optional terminal name. You can display the login and terminal names of the users who are logged in on your system by who, w, or finger.

To establish two-way communication with another user, you and the other user must execute write, specifying the other’s login name as the *destination-user*. The write utility then copies text, line by line, from one keyboard/display to the other (Figure 3-15). Sometimes it helps to establish a convention, such as typing oo (for over) when you are ready for the other person to type and typing oo (for out and in) when you are ready to end the conversation. When you want to stop communicating with the other user, press CONTROL-D at the beginning of a line. Pressing CONTROL-D tells write to quit, displays EOF (end of file) on the other user's terminal, and returns you to the shell. The other must do the same.

If the Message from ... banner appears on your screen and obscures something you are working on, press CONTROL-L or CONTROL-R to refresh the screen and remove the banner. Then you can clean up, exit your work, and respond to the person who is writing you. You just have to remember who is writing you, as the banner will no longer be on your screen.

Refer to “Write Daemon” on page 331.

# talk: Communicates with Another User

You can use the talk to carry on a two-way conversation with another person who is logged in on your system. You can also use talk to communicate with someone on a different computer. The talk utility splits your screen into two sections; once you establish contact with the other person, the messages you type appear in the top half of screen, and the messages from the other person are displayed in the bottom half. Each keystroke appears as you type it. In this example Alex needs some information from Jenny:

```
$ talk jenny
```

```
$ write Alex
Hi Alex are you there? o
Message from alex@bravo.tcorp.com on pts@0 at 16:23 ...
Yes Jenny, I'm here. o
```

**Figure 3-15** The write utility II