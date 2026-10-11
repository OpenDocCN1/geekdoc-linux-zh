```
#
#
# Do not allow this known spammer to use the mail gateway
in.smtpd: SPAMMER, junkmail.spam.com
# A truly paranoid sysadmin
ALL: ALL
# End of hosts.deny.
```

# Network Insecurity Files

UNIX operating systems, including Linux, are extremely trustworthy – in the technical sense – but you may have to curtail the system's eagerness to trust other systems. Some UNIX files enable your network to trust other hosts, even without passwords. They are the `.rhosts` and the `/etc/hosts.equiv` files.

All such files function in much the same way: They trust a host (and possibly a user) on the basis of name alone. The `.rhosts` file is found in user accounts, where the `/etc/hosts.equiv` applies these rules system-wide.

The syntax for these files is simple:

```
trustedhost trusteduser
```

If you want to trust all the hosts, place a plus "+" where the hosts go; if you want to trust all users, place a plus "+" in the users' field.

![](bbox=[0.05, 0.58, 0.15, 0.65])

Under no circumstances should you put a `.rhosts` with "+" or "*+*" in the root directory. This also applies to the `/etc/hosts.equiv`.

Suppose you find a file on your system in a user's home directory that looks like this:

```
tigerlair stripes
myopia +
+ bob
```

Apparently this user is not prompting user *stripes* on the host *tigerlair*. He is also allowing anyone from the *myopia* host on his account – and letting anyone with the username *bob* have access to his system – without prompting for passwords. Big trouble lurks in these three lines of code.