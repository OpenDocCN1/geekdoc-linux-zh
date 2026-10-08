The following command lists the largest 20 mailboxes and mails the result to root. It is suitable for use in root's crontab.

```
ls -ss /var/spool/mail | head -20 | /bin/Mail -s mailboxes root
```

# 3.3 Telnet

![](bbox=[0.068, 0.223, 0.952, 0.283])

Telnet has two problems. All of a user's data is sent unencrypted so that anyone sniffing the network anywhere between your system and the other system will see all the data. It is also vulnerable to a "Man-in-the-middle attack."

The worse is that the password used to log in the server is in clear text. Assume that the V.P. of Finance downloaded an archive of jokes. A cracker could have sniffed his password. He now might be in the V.P.'s account, reading his confidential files containing bank account numbers, the planned IPO (Initial Public Stock Offering), and details on that great new idea that could make the company millions of dollars.

An additional problem is that a cracker can try guessing each user's telnet password with as many times as he wants because telnet does not track the number of incorrect guesses. These bad guesses will end up in the list files. See "An Example for Automatic Paging" on page 358 for a description of how to be arranged as soon as someone enters a bad telnet password.

Moreover, telnet uses the user's login password if shadow passwords are not being used and a cracker gets a copy of /etc/passwd, then the cracker can crack the password on his own system and use telnet without the delay and risk of discovery of repeatedly sending password guesses to your system.

A proper solution is to require your users to use SSH for data that leaves protected networks and to enforce this by configuring the firewall to block telnet's port in each direction. Requiring people to use SSH instead of telnet internally will also protect against crackers, including any inside the organization, getting into your internal network and sniffing internal data from there. Removing telnet and telnetd will help here. Another option is using stelnet, an SSL-wrapped telnet solution.

# 3.4 FTP

![](bbox=[0.068, 0.823, 0.952, 0.883])

FTP suffers from most of the same problems as telnet and the solution is the same. Replace it with SSH (for most nonanonymous use). SSH2 offers sftp, a introduced