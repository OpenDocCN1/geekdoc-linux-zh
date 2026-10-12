This will allow any user from the specified host to login to the system if the userid exists on the local system.

```
hostname -userid
```

The preceding will allow all but the named userid on the specified host to login if that userid exists locally.

This is true for all users except root. Root must have a .rhosts file (explained in ".rhosts" later in the chapter) in his home directory with remote users and hosts for this to work.

Having entries in hosts.equiv can be dangerous—if any of the hosts in your hosts.equiv file are hacked, the hacker has an easy way to get a shell on your system. If you must use rsh/rexec/login, be sure to configure /etc/pam.d/rexec, etc/pam.d/rsh, and /etc/pam.d/rlogin to make there is a line in there to add the pam_rhosts_auth.so module. This will perform some checks such as making sure that the user's .rhosts file is not writable by anyone other than the owner, and ignoring the "+" entry in hosts.equiv and .rhosts (allow all access). If you would like the system to only use /etc/hosts.equiv and not .rhosts, add the no_rhosts argument to the pam_rhosts_auth.so line.

# ftpusers

ftpusers stores the names of local users who cannot use the ftpd service. When ftpd is invoked by inetd/tcpd in response to a network request, ftpd checks this file to make sure that the user is allowed to use FTP. At the very least you should have root in this file. Not allowing root to use FTP is a good idea because it removes yet another potential point of entry for the superuser account. You should also put all other names into this file that exist in /etc/passwd that should never use FTP, such as bin, sys, daemon, adm, and so on. In addition, some actual users might not have a need for ftp and they should also be included in this file.

# ftphosts

This is another access control list for ftpd. It allows you to set permissions specifically for connection to the ftp service. The format is

```
allow|deny <userid> <address, address, ...>
<userid> is any user name.
<address> is one of host.domain, IP:netmask, IP/maskbits, or netbits.*
```