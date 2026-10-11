# **Example 11-16** Failed Authentication Due to IgnoreRootRhosts

```
[root@underdog /root]#ssh -o RhostRSAAuthentication=no pluto
root@pluto's password: 
Last login: Thu Jul 1 16:12:49 1999 from underdog
No mail.
[root@pluto /root]#
```

Notice that sshd on pluto prompts for the root password on pluto. There is no indication that Rhosts and RSA Authentication failed, nor why. Let's see if the log file tells us anything. Example 11-17 shows the log file entries that correspond to Example 11-16.

# **Example 11-17** Log Messages Corresponding to Example 11-16

```
Jul 1 16:14:11 topcat sshd[15022]: debug: Forked child 15025.
Jul 1 16:14:11 topcat sshd[15025]: connect from underdog
Jul 1 16:14:11 topcat sshd[15025]: log: Connection from 10.13.1.9 port 1022
Jul 1 16:14:11 topcat sshd[15025]: debug: Client protocol version 1.5; client
software version 1.2.27
Jul 1 16:14:11 topcat sshd[15025]: debug: Sent 768 bit public key and 1024 bit
host key.
Jul 1 16:14:11 topcat sshd[15025]: debug: Encryption type: blowfish
Jul 1 16:14:11 topcat sshd[15025]: debug: Received session key; encryption
turned on.
Jul 1 16:14:11 topcat sshd[15025]: debug: Installing crc compensation attack
detector.
Jul 1 16:14:11 topcat sshd[15025]: debug: Attempting authentication for root.
Jul 1 16:14:16 topcat sshd[15025]: log: Password authentication for root
accepted.
Jul 1 16:14:16 topcat sshd[15025]: log: ROOT LOGIN as 'root' from underdog
```

While the log file tells us that root successfully passed password authentication, it doesn't tell us that Rhosts and RSA Authentication failed. At this point, we don't even know if Rhosts and RSA Authentication was attempted. In order to get more information, we need to run sshd in debug mode on the server. Example 11-18 provides a way to accomplish this. Note that sshd is killed prior to running sshd -d. If this is not done, you will get an error message indicating that sshd are already running. The entries in bold represent the information we seek. They tell us that Rhosts and RSA Authentication was attempted, but failed. So, if we were really debugging, we could concentrate our investigation on the server configuration (and hopefully find the IgnoreRootRhosts entry). Note that sshd -d may be used to debug SSH connections generally and not just specifically with Rhosts and RSA Authentication.

# **Example 11-18** Using sshd -d

```
[root@topcat]# /etc/rc.d/init.d/sshd stop
Stopping sshd: sshd
[root@topcat]# sshd -d
debug: sshd version 1.2.27 [1696-unknown-linux]
debug: Initializing random number generator; seed file /etc/ssh/ssh_random_seed
log: Server listening on port 22.
log: Generating 768 bit RSA key...
Generating p:
..................++ (distance 1214)
Generating q:
....
++ (distance 430)
Computing the keys ...
```