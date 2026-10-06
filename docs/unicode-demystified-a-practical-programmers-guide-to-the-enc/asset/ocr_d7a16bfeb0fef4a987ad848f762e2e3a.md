# Comparison of w, who, and finger

| Information Displayed | w | who | finger |
| --- | --- | --- | --- |
| User login name | X | X | X |
| Terminal-line identification (tty) | X | X | X |
| Login day and time | X | | X |
| Login date and time | | X | |
| Idle time | X | | X |
| What program the user is executing | X | | |
| Where the user logged in from | | | X |
| CPU time used | | X | |
| Full name (or other information from /etc/passwd) | | | X |
| User-supplied vanity information | | | X |
| System up time and load average—use up-time for this information only | X | | |

# Communicating with Other Users

The utilities discussed in this section exchange messages and files with other users either interactively or through e-mail.

# write: Sends a Message

The write utility sends a message to another user who is logged in. When you and another user use write to send messages to each other, you establish two-way communication. Initially a write command (Figure 3-14) displays a banner on the other user's terminal, saying that you are about to send a message.

```
write destination-user [terminal]
```