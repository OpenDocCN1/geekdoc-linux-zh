starting the mail -f aspect of mail, he can review and deal with these messages in the same way he dealt with the new or unread messages in /var/spool/mail/panzasan by using mail. Figure 3.1 illustrates a typical mail reception and storage process.

# ## Sending Messages to the Screen: write and wall Commands

Both of the commands discussed in this section provide the capability to contact other users on the system:

+   - **write** enables you to contact one or more specific users
+   - **wall** enables you to contact all users on the system

Let's discuss each in turn.

# ### The write Command

The mail command showed us how to send messages to others' mailboxes and how to receive and manipulate messages in our mailbox. By contrast, the **write** command displays a message immediately on the specified user's screen. You can send messages to a user on the local system or on another system on the network (simply replace **username** with **username@hostname**). If, by using who or finger, you determine that your target user is logged in on more than one terminal, you can display your message on all the terminals unless you just want to specify the terminal(s) to which you want your message to be sent, as follows:

```
$ write username ttyname/number<Enter>
```

Otherwise, to reach the target user on any and all terminals, the syntax is just the following:

```
$ write username<Enter>
```

For a specific user to receive the message, however, he or she must be logged in at the time and must not have refused permission for the message to appear on his or her terminal. By default, Linux does not turn off the **write** permission; that task is accomplished by the user with the **msg** command (covered later in this chapter).