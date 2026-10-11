```
@                 WARNING: UNPROTECTED PRIVATE KEY FILE!           @
@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@
Permissions 0640 for '/root/.ssh/id_rsa' are too open.
It is required that your private key files are NOT accessible by others.
This private key will be ignored.
Load key "/root/.ssh/id_rsa": bad permissions
agonzalez@192.168.122.43's password:
```

The protocol SSH allows to forward remote and local ports that are useful to access internal services from outside. Option -L is used to map a local port to an IP and port from the remote network using the SSH tunnel. Option -R is less used, and its functionality is to expose an IP and port from the local network to the remote server connected with SSH. *Figure 9.19* shows the traffic flow using an SSH port forwarding:

![](bbox=[0.13, 0.35, 0.87, 0.53])

With SSH as well, it is possible to forward the graphical applications using the **X11 forwarding** mechanism. Using option -X in the *SSH client*, it is possible to execute applications in the remote server showing the graphical interface in the client node. Refer to *figure 9.20* for an example:

```
[agonzalez@server ~]$ ssh -X agonzalez@192.168.122.43
agonzalez@192.168.122.43's password:
agonzalez@ubuntu:~$ xeyes
```

![](bbox=[0.13, 0.72, 0.87, 0.88])

# SSH public and private keys