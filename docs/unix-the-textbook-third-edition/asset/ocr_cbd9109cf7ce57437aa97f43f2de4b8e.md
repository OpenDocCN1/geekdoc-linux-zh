The other user needs to execute the talk command to respond to you. That establishes a communication channel, and both users’ display screens are divided into two halves. The upper-half contains the text that you type, and the lower half contains the other user’s responses. Both you and the other user can type simultaneously. The talk command simply copies the characters that you type at your keyboard on the screen of the other user. The chat session can be terminated when either of you presses <Ctrl+L>. If you are using the vim editor and your screen is corrupted during the communication, you can use <Ctrl+L> to redraw the screen.

Suppose that user sarwar wants to talk to another user, bob, and that both are logged on to the same host. The following command from sarwar initiates a talk request to bob.

```
$ talk bob
```

As soon as sarwar hits <Enter>, the following message is displayed at the top of bob’s screen.

```
[Waiting for your party to respond]
Message from Talk_Daemon@upibm7.egr.up.edu at 13:36 ...
talk: connection requested by sarwar@upibm7.egr.up.edu.
talk: respond with: talk sarwar@upibm7.egr.up.edu
```

When bob runs the talk sarwar command, both bob’s and sarwar’s screens are divided in half, with the upper halves containing the message [Connection established] and the cursor moved to the top of both screens. Both bob and sarwar are now ready to talk. If bob wants to ignore sarwar’s request while using a shell, he can simply press <Enter>.

If bob is logged in on another host—say, upsun29—sarwar needs to run the following command to initiate the talk request.

```
$ talk bob@upsun29
```

If sarwar is logged in once on upibm7 and bob wants to communicate with sarwar, his response to the preceding request should be talk sarwar@upibm7. If bob is logged in on upsun29 multiple times, the following command from sarwar initiates a talk request on terminal tty p2 (one of the terminals bob is logged on to).

```
$ talk bob@upsun29 tty p2
```

If you want to block all talk requests because users keep bothering you with too many requests, execute:

```
$ mesg n
$
```

This command works only for your current session. If you want to block all talk and write requests whenever you log on, put this command in your ~/.profile file on Solaris or