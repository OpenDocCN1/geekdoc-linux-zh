```
```
lock
crtscs
modem
login
```
```

+   3. Create a file called /etc/ppp/options.port, where port is the port file, such as ttyS0 for the first serial port. This file contains the IP address or hostname of the PPP server followed by a colon (: ) and the IP address or hostname of the PPP client. You should be sure that the PPP client hostname is available for use on the network. For instance:

```
```
192.168.1.1:192.168.1.200
```
```

+   4. Create an /etc/ppp/pap-secrets file entry for any users who should be able to use the PPP link. This entry is similar to the one for dial-out PPP access, but it lists a local username and password. For instance, the following allows the user abell to connect to a PPP server using the password watson:

```
```
abell * watson
```
```

+   5. Check the permissions on the pppd file. You should set its UID root by typing chmod u+s /usr/sbin/pppd, if necessary. When you’ve done this, typing ls -l /usr/sbin/pppd should reveal the following permissions:

```
```
-rwsr-xr-x   1 root   root   140656 Mar   7 10:25 /usr/sbin/pppd
```
```

+   6. To run pppd, users dialing in must normally type a slightly cumbersome command—it’s not very complex by Linux system administration standards, but it’s a bit of an annoyance. You can reduce the annoyance factor by setting up a global alias to run this command. Once set up, a user need only type ppp to launch pppd on Linux. You can set this up by entering the following line in /etc/bashrc (assuming your user’s account is configured to use Bash as the default shell):

```
```
alias ppp="exec /usr/sbin/pppd -detach"
```
```

With these steps followed, a user should be able to use PPP to connect to the computer and any network to which it’s attached. The PPP server requires manual login via a standard Linux login: prompt, after which the client must type ppp to start pppd on the Linux system. This can all be handled with a login script or by a manual procedure from some PPP dialers, such as the one that comes with Microsoft Windows.

# Receiving Faxes

If you’ve configured your system to accept dial-up text-mode logins using mgetty, as described in "Accepting Text-Mode Logins," your system is automatically configured to receive faxes. When a call comes in on the line to which the modem is attached, the modem determines whether the call is a data call or a fax call. If it’s a data call, mgetty passes control of the serial line over to appropriate programs to handle data transmission. If the modem detects an incoming fax, mgetty initiates fax reception and places incoming faxes in the /var/spool/fax/incoming directory.

Incoming fax files use the standard G3 fax file format. You can view these files with several programs, such as KDE’s KFax (shown in Figure 11.8). Such programs are typically quite simple; they allow you to view or print the file, but not much else.