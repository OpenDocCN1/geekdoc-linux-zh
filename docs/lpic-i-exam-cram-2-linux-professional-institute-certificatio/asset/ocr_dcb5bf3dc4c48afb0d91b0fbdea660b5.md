When you press Enter to execute the command, a message appears on rbrunson's console that he is receiving a message from the root user on console /dev/tty1 at 15:51. Then when the root user types a message and presses Enter, that text appears on the user's console. The conversation is ended when the sender presses Ctrl+D.

# Talking to Users

The talk command is useful for two-way communication with a user, allowing for what is essentially a chat session between two users.

The talk command works locally on the machine with logged-in users or from machine to machine, as long as the users are logged in with the target username.

To initiate a talk session with the user snuffy who's logged in to the console of the server/machine, you would type the following command as the root user:

```
talk snuffy tty1
```

This pops up a message on snuffy's console that a connection is requested by the root user on the machine and tells snuffy to type talk root@localhost and press Enter. This puts the root user and snuffy into a chat mode, with the root user's information on the top of the screen and snuffy's replies on the bottom of the screen.

You might have to set the msg options to allow messages to appear on your screen. The msg y command sets the console to allow connections and messages. However, it causes all sorts of system and other user spam to show up, so you might want to set it to msg n.

Additionally, you have to enable the ntalk daemon via the chkconfig utility. Or you might need to edit the /etc/xinetd.d/talk script so the line that contains disabled = yes reads disabled = no. This enables the daemon to start a request for a talk session.

> You will see motd and the issue files on the exam, and reportedly write, talk; and msg appear sporadically.

Lastly, the wall, or write all, command sends a message to all the users on the system consoles and remote consoles.

To send a wall message to every user that the system is going down in 5 minutes, you would use

```
wall "System going down in 5 minutes"
```