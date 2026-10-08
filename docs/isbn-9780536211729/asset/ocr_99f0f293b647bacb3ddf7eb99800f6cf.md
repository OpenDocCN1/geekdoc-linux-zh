# Replace These Weak Doors with Brick

The login process (and telnet and ftp) will very carefully prompt someone for a password after she entered a bogus account name, even though that password will be ignored. This prevents from guessing account names as the indication is the same (login incorrect) regardless of whether the account name or password is incorrect.

By preventing a cracker from finding out account names, cracking becomes much harder because he must correctly guess the account name and password at once. This is a combinatorial nightmare. This also prevents account name guessing for passwords.

The finger facility breaks this out a cracker has to do finger expenta-corp. where x is dave, joe, smith, jones, and so on for the most common names.

In ways finger could be helpful, being able to provide users addresses and phone numbers using this method, but e-mail has largely replaced it. The bit about "unread e-mail" is so you will know if a user has read the urgent e-mail you sent.

Finger dates back to the early days of ARPANET when only scientists, professors, and graduate students had access. It is not appropriate for the Internet unless your confidence in security is high enough you do not mind the world knowing when your people are at the office or at home. (It helps crackers to know when it is safer to try crack a system because there is nobody on it notice.)

The finger service is controlled by an entry in the /etc/inetd.conf; it is turned by default. You will probably want to edit the inetd.conf file and comment the line for the finger service. The file to be edited somewhat like the following.

```
finger stream tcp nowait nobody /usr/sbin/tcpd.finger
```

To disable the finger service, insert a "#" at the start of the line (which makes this a comment) and save the file. To enable your change immediately type

```
killall -HUP inetd
```

As an alternative, you could make use of TCP Wrappers to restrict its use in your organization by editing /etc/hosts.allow to restrict finger use. This is discussed in "TCP Wrappers" on page 112. IP Tables could be used instead.



![](bbox=[0.275, 0.725, 0.515, 0.765])

The rwh daemon is a process that allows a remote user to see who is logged into your system. The client program is finger. It has many of the security problems of finger.

+   23. They will spend the computrons to encrypt the password as they were going to compare the encrypted version in /etc/passwd or /etc/shadow.

This is to prevent a cracker from noticing the difference in time before saying Login incorrect depending on whether the account exists. This lesson too learned the hard way.