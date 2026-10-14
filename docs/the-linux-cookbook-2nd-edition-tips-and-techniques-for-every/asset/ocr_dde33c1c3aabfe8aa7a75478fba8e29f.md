# 34.7.1 Sending a Message to Another User’s Terminal

There are a few ways to do this, depending on whether you are sending to a particular user or to all users.

# METHOD #1

Use `write` to write a message to the terminal of another user. Give the username you want to write to as an argument. This command writes the message you give, preceded with a header line indicating that the following is a message from you, and giving the current system time. It also rings the bell on the user’s terminal.

+   ⇒ To send the message “Wake up!” to the terminal where user sleepy is logged in, type:

```
```text
$ write sleepy
Wake up!
^D
$
```
```

The other user can reply to you by running `write` and giving your username as an argument. Traditionally, a user ended a `write` message with -o, which indicated that what he was saying was “over” and that it was now the other person’s turn to talk. When a user believed that a conversation was completed, he would end a line with “oo,” meaning that he was “over and out.”

# METHOD #2

A similar command, `wall`, writes a text message to all other users on the local system. It takes a text file as an argument and outputs the contents of that file; with no argument, it outputs what you type until you type `CTRL-/D` on a line by itself. It precedes the message with the text “Broadcast message from username” (where username is your username) followed by the current system time, and it rings the bell on all terminals it broadcasts to.

+   ⇒ Here are two ways to use this.
+   
+   - To output the contents of `/etc/motd` to all logged-in terminals, type:
+     ```text
+     $ wall /etc/motd
+     ```