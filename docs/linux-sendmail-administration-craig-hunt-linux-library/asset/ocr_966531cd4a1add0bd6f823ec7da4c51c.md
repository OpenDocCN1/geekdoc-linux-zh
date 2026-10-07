# Listing 12.1 Running the imaps Service from xinetd

```
service imaps
(
    socket_type = stream
    wait = no
    user = root
    server = /usr/sbin/stunnel
    server_args = -1 /usr/sbin/imap --imapad
    log_on_failure += USERID
)
```

stunnel, however, has nothing specific to POP, IMAP, or e-mail. It can be used to secure a wide variety of daemons. The stunnel map provides for more details about stunnel. Linux Security by Ramon Hontañón (Syex, 2001) for more information about securing a variety of services.

The primary reason for running POP or IMAP through stunnel is to ensure that the user's password cannot be stolen from a POP or IMAP session and then used by the thief to log in to the server. stunnel encrypts everything: the login and the download of mail. This guarantees that the contents of the mail cannot be surreptiously viewed by a snooper during the download, but from the point of view of the system administrator securing the content of the mail is usually unimportant. In all likelihood the mail moved through the Internet to the server. Encrypting as it moves from the server to the reader is a little silly after the worldwide exposure the mail has already received. The password is really the only piece of information you want to protect. Using a stronger form of authentication than simple clear text passwords can protect it. POP provides strong authentication through the optional APOP command of the POP3 protocol.

To offer the APOP command for your POP3 clients, you must install a daemon, such as Qualcomm's Qpopper, which implements the command. Qpopper is available as an RPM from many Linux vendors and can be located through rpmfind.net. Once you install it, make sure that the entry for pop in inet.conf or xinetd.conf points to the new in.qpopper program. The Qpopper package adds a program named popauth that to create passwords for the APOP command. Listing 12.2 shows how an administrator adding an APOP password for the user craig.

# Listing 12.2 Using the popauth command

```
[root]# popauth -user craig
Changing only APOP password for craig.
New password: SecretPassword
Retype password: SecretPassword
```