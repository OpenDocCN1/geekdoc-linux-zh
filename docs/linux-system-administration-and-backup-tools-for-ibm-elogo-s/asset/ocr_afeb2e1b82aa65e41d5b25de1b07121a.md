Once all your system configuration files are set up you should have a working network. You should reboot your network to verify that the system is loading the files properly on boot.

# 4.4.4 Enabling remote services to your server

In order to enable certain types of remote access to your system, Linux may require some additional configuration to be done.

The /etc/services file lists which kind of services you are going to make available on which ports. A partial listing of the file is shown in Figure 74. You will notice that each service is assigned a number. You will note that FTP is assigned 21, and telnet is assigned 23.

```
#partial listing of /etc/services
#
discard     9/tcp      sink null
discard     9/udp      sink null
systat     11/tcp     users
daytime     13/tcp
daytime     13/udp
netstat    15/tcp
gsqd        17/udp
mp         18/tcp      # message send protocol
mp         18/udp      # message send protocol
chargen    19/tcp      ttytst source
chargen    19/udp      ttytst source
ftp-data   20/tcp
ftp         21/tcp
fsp        21/udp      fspd
ssh         22/tcp      # SSH Remote Login Protocol
ssh         22/udp      # SSH Remote Login Protocol
telnet      23/tcp
# 24 - private
# 26 - unassigned
smtp        25/tcp      mail
time        37/tcp      timserver
time        37/udp      timserver
rlp         39/udp      # resource location
ameserver  42/tcp      name
                            # IEN 116
(The remainder of file is not displayed)
```

Figure 74. /etc/services file partial listing

However, you cannot do a telnet or any type of remote access into a system unless the service is activated. It is controlled by files in the /etc/inetd.directory.