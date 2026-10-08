
# THE r TOOLS 429

rsh on the local computer. This is a peculiarity of the GNU getopt which is used for evaluation of command line options and parameters.

If users have different accounts (for example hein on one and jhein on the other computer), you can use the -l to specify any user ID before the computer name from which a login should be possible. Useful options are -8 for an 8-bit-capacity sequence and -E for switching off the special treatment of the escape character (usually the tilde (~)). The option -e can be used to specify a replacement character for this.

```
(Linux):> rsh -- pea -l -d bin
drwxrxr-xr-x 2 hein staff 512 Jul 26 16:22 bin
```

- **Listing 16.4** Execution of programs on remote computers with rsh.

Some rlog daemons allow specification of + in .rhosts files. This allows users with the same user name to log in, no matter from which computer they are calling login. For reasons of security, this kind of entry should be avoided; some daemons ignore this entry.

Listing 16.5 shows an example of the file ~/.rhosts. This file should only be readable for individual users. Each line describes a computer from which arsh, login or rcp without password is possible. As the computer name, you should specify the first entry from the file /etc/hosts or the Fully Qualified Domain Name (FQDN). If you have different IDs on the computers, you can then enter a user name.

```
corn.example.org hein
pea.example.org jhein
```

- **Listing 16.5** An example of the file ~/.rhosts.

The system administrator can set up computers (in a local network) as having equal rights by entering the names of all local computers in the file /etc/hosts.equiv (Listing 16.6) of each computer. However, this makes sense only for networks in which computers and users are centrally managed.

The file /etc/hosts.equiv is not used for accesses by the user ID root, so in this case an additional ~/.rhosts file is required. In a local network which is to be centrally managed, this can significantly facilitate things, because, for example, it allows use of rdist (see Section 16.6).

# 430 NETWORK APPLICATIONS

```
corn.example.org
-carrot.example.org
cabbage.example.org  sven
```

Listing 16.6 The file /etc/hosts.equiv.

The first entry in Listing 16.6 ensures that every user (except for root) can log in from corn.example.org using login without a password. The second entry requires a password for each login from carrot.example.org, no matter what individual users have entered in their ~/.hosts. The third line allows user sven on cabbage.example.org without a password as an arbitrary user (except root).

This method is based on the fact that by means of incoming packets (namely the sender's address) the correct sender (computer) can be identified. However, this is not always the case, because with IP or DNS spoofing another sender's address or another host name can be specified. Thus, if security considerations play a major role, this method would not be recommended. This applies in particular if the access is carried out on or from the external computer. Consequently most firewalls seem to block these services.

A disadvantage of rsh is that no tty is associated with the program. Thus, programs such as vi cannot be started with rsh. Instead, you need to log in, for example, with login. If you receive error messages as '$TERM is not defined' (from setterm) or 'stty: invalid argument' (from stty) when using rsh, you must adapt your login scripts accordingly. Listing 16.7 shows some sample adaptations for the tsch, Listing 16.8 shows the corresponding adaptations for the bash. This can be used to prevent the commands stty or setterm being called although no tty is available.

```
tty -s
if ( $status == 0 )
  stty pass8
endif
```

Listing 16.7 Adaptations in ~/.login.

# THE r TOOLS 431

```
tty -s
if [ $? = 0 ]; then
    stty pass8
endif
```

**16.8** Adaptations in rsh, ~/.profile.

On the basis of rsh, a protocol called restart was developed for X which facilitates the start of X programs on other computers. Both the current value of the DISPLAY variable and the authorization (see Section 6.6) for the X server are transmitted. This, however, requires the restart daemon which is usually running only on few computers.

Another alternative is provided by the xon program which is also based on rsh, but does not require an additional daemon. However, if you want to use xauth for authorization of X accesses, this must be done separately. An example is shown in Listing 16.9.

If you are using ssh (see Section 16.4), it is no longer necessary to use xhost or xauth. Shell redirection and authentication are taken over by the secure shell. This method is very stable. It is not easy to generate and manage the correct DISPLAY variable by means of a shell script.

```
xauth extract - DISPLAY | rsh RemoteHost xauth merge -
```

**16.9** Transferring the X authority by means of rsh.

The protocol used in rsh is documented in [rfc1258]. In this case, the RFC is only used for the documentation of an implemented and used protocol.

# 16.3.2 Login on remote computers

With the login (remote login) program, you can run an interactive session on a remote computer. If no command is specified with rsh, a login is carried out automatically, assigning the shell a tty. If you specify a program with rsh that needs a tty (such as vi), you will receive an appropriate error message.

Logins instead of telnet are used on UNIX computers because with an appropriate configuration (as rsh) no password needed be entered. The rlogin program is the only one of the r tools that asks for a password if a login without password is not possible.

The security considerations are the same as rsh. This protocol is defined in [rfc1282]. In contrast to rsh and rcp which deny access, rlogin

# 432 NETWORK APPLICATIONS

asks for a password when no valid ~/.hosts entry is found. As with rsh option -l may be used to specify another user name.

If the login program is called with the name of a computer, a connection to this computer is automatically established. Thus you can, for example, create a symbolic link to the login program for each target computer. In my own login scripts, I define an alias for each frequently used computer.

# 16.3.3 File transfer

The program rcp (remote copy) is used to copy files between two computers on each of which you need valid user ID. The name of the remote computer is followed by a colon (:) and the name of the file or the target directory. A different user ID can be specified by prefixing the computer name with the user name followed by an @ sign (see Listing 16.10). The authorization is carried out via the same mechanism as rsh or login.

```
rcp netrc pea.example.org:
rcp netrc user@veggies.example.org:
rcp user1@host1:file1 user2@host2:file2
```

Listing 16.10 Copying files in the network with rcp.

On older UNIX systems, the cp command is not capable of copying subdirectories recursively, the rcp -r command can be used instead. cp always copies all specified files. For the purpose of synchronization between directories on different computers, the rdist command is used. This program deletes files that no longer exist on the source computer and transfers only files that have changed. Especially when updating larger directory trees in which little has changed, the network load with the use of rcp is much higher than it should be.

# 16.3.4 Logged-in users in the local network

Often, a network consists of a number of computers. If you are looking for a specific user, for example to address this person by means of talk, it is difficult and long-winded to issue on all computers or to start the finger program for all possible computers.

If the administrator has started the rhod daemon on all computers of the local network, you can use the rwho command to obtain a list of all active, logged-in users (Listing 16.11). With the command runtime (Listing 16.12)
