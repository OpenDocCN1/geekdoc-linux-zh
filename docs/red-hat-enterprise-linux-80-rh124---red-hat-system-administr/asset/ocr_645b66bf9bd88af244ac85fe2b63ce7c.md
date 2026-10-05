# GUIDED EXERCISE

# CONFIGURING HOST NAMES AND NAME
RESOLUTION

In this exercise, you will manually configure the system's static host name, /etc/hosts file,
and DNS name resolver.

# OUTCOMES
Should be able to set a customized host name and configure name resolution settings.

# BEFORE YOU BEGIN
Log in as the student user on workstation using student as the password.

From workstation, run the lab net-hostnames start command. The command runs a
start script that determine if the host, server, is reachable on the network.

```
[student@workstation ~]$ lab net-hostnames start
```

+   1. Use the ssh to log in to server as the student user. The systems are
configured to use SSH keys for authentication, so a password is not required to log in
servera.

```
[student@workstation ~]$ ssh student@servera
[student@servera ~]$
```

+   2. View the current host name settings.
2.1. Display the current host name.

```
[student@servera ~]$ hostname
servera.lab.example.com
```

+   2.2. Display the host name status.

```
[student@servera ~]$ hostnamectl status
Static hostname: n/a
Transient hostname: servera.lab.example.com
Icon name: computer-vm
Chassis: vm
Machine ID: 7a2b1a4e278e48b9f80e80714aabcd05
Boot ID: 76b1a3d0c944a94445af778cb08f749
Virtualization: kvm
Operating System: Red Hat Enterprise Linux 8.0 Beta (Outpa)
PE OS Name: cpe:/redhat/enterprise_linux:8.0-beta
```