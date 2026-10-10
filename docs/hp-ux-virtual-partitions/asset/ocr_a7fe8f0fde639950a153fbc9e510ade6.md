```
$ telnet a4410750
```

or

```
$ telnet hp1
```

Similarly, either of the following Berkeley commands works:

```
$ rlogin a4410750
```

or

```
$ rlogin hp1
```

# */etc/hosts.equiv*

Your system may be setup so user's don't have to issue a password when they **rlogin** to a remote system. they can set up equivalent hosts by editing this file. As I mentioned earlier, this is technique sometimes considered a security risk, so it is not always employed. The login names must be the same on both the local and remote systems for/*etc/hosts.equiv* to allow the user to bypass entering a password. You can either list all the equivalent hosts in/*etc/hosts.equiv* or list the host and user name you wish to be equivalent. Users can now use **rcp** and **remsh**, because they are equivalent users on these systems. I usually just enter all the host names on the network. Here is an example of/*etc/hosts.equiv*:

```
a4410730
a4410tu1
a4410tu2
hpnterm1
a4410827
a4410750
```

Keep in mind the potential security risks of using/*etc/hosts.equiv*. If a user can log into a remote system without a password, you have reduced the overall level of security on your network. Even though