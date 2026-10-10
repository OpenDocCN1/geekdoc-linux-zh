# # Sending and Receiving Mail: mail Command

The mail command is interactive and is used to both send and receive mail messages.

# ## To Send Mail

To send a message to another user on the same system, the format is

```
$ mail username<Enter>
```

To send a message to more than one user on the same system, enter all user names after the mail command, separating each by one space:

```
$ mail username1 username2<Enter>
```

To send a message to a user on another system, type the username followed by @ and the name of the system:

```
$ mail username@hostname<Enter>
```

To send a message to more than one user on another system, separate each username@hostname entry by one space.

Example 3.11 shows how one user can send mail to another user on the same system (that is, on the same host) and to one on a different system. Notice that whenever the mail command is invoked, the system responds with a Subject: prompt. Type a description line that will appear in the receiver's list of incoming mail, and then press Enter again. Now you can type whatever you want to communicate to the receiver.

When you have finished your message, press Enter and then press the combination Ctrl-D. The system responds with a Cc: prompt. If you want to send copies of the message to others, type their usernames. When you are finished, press Ctrl-D again. The system sends the message and responds with a shell prompt (usually $ and a cursor).

**Example 3.11 Sending Mail with the mail Command**
Knowing that Sancho is on the system today, Don Quixote sends a message to him: