Because of its user-friendly interface, it is suitable for your Linux users who are not yet friends with Linux.

# rlogin

Syntax:

```
rlogin [-l username] host
```

The rlogin command allows you to log in to a host remotely. For example, to log in to a host called shell.myhost.com, run

```
rlogin shell.myhost.com
```

Because rlogin is not considered safe, I recommend that you use it only in a closed LAN environment. The -l option allows you to specify a user-name to be used for authentication. If you want to log in to a host remotely without entering a password, create an .rhosts file in the user's home directory. Add the host name or IP address of the computer that you will use to issue the rlogin request. Again, because this is considered a security risk by many, I do not recommend wide use of rlogin.

# talk

Syntax:

```
talk username tty
```

If you need to send a message to another user, e-mail works fine. But, if you need to communicate with another user in real time, similar to a telephone conversation, use the talk command. To talk to another user who is logged in, use the following command: talk ronak@csus.edu The user who you request has to accept your talk request. After the user accepts your talk request, you can begin talking (typing) to each other. The talk program is terminated when either party executes Ctrl+C (the intr key).