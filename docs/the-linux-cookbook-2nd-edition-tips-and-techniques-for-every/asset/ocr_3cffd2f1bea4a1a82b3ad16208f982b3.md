+   To output the text "Who wants to go out for Chinese food?" to all logged-in terminals, type:
+   $ wall [RET]
+   Who wants to go out for Chinese food? [RET]
+   [CTRL]-D

# 34.7.2 Denying Messages to Your Terminal

You can control write access to your terminal for commands like write and wall, so that you aren't interrupted. Do this with mesg. It works like biff (see Recipe 32.4.2 [Setting Notification for New Mail], page 624): With no arguments, it outputs whether or not it is set; with y as an argument, it allows messages to be sent to your terminal; and with n as an argument, it disallows them.

The default for all users is to allow messages to be written to their terminals; antisocial people usually put the line mesg n in their .bashrc file (see Recipe 3.7.3 [Using Shell Startup Files], page 86).

+   To disallow messages to be written to your terminal, type:
+   $ mesg n [RET]
+   To output the current access state of your terminal, type:

```
$ mesg [RET]
is n
$
```

In the preceding example, mesg indicated that messages are currently disallowed to be written to your terminal.

# 34.7.3 Chatting Directly with a User

Ytalk
DEB: ytalk
RPM: ytalk
WWW: http://www.iagora.com/~espel/ytalk/ytalk.html

Use talk to interactively chat in realtime with another user. Give the username (or email address) of the user you want to chat with as an argument; a message will be sent to that user's terminal, indicating that a connection