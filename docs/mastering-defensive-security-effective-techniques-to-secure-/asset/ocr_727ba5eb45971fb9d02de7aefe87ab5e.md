# Hardening a Unix Server

Also, in the following figure, notice after issuing this command, the + sign was also removed at the end of the permissions (the result of $ls -l):

```
kali@kali~$ ls -l
total 44
-drwxrwx 2 kali kali 4096 Nov 29 18:01 akira
-drwxr-xr-x 2 kali kali 4096 Nov 30 00:25 bravito
-rw-r--r-- 1 kali kali 0 Nov 30 00:01 bravo
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Desktop
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Documents
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Downloads
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Music
-drwxr-xr- 34 kali kali Oct 03 03:05 output
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Pictures
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Public
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Templates
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Videos
kali@kali~$ setfacl -b bravo
kali@kali~$ ls -l
total 66
-drwxr--- 2 kali kali 4096 Nov 29 18:01 akira
-drwxr-xr-x 2 kali kali 4096 Nov 30 00:25 bravito
-rw-r--r-- 1 kali kali 0 Nov 30 00:01 bravo
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Desktop
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Documents
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Downloads
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Music
-drwxr-xr- 34 kali kali Oct 03 03:05 output
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Pictures
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Public
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Templates
-drwxrxr-x 2 kali kali 4096 Jul 27 13:34 Videos
kali@kali~$ setfacl bravo
```

Figure 7.23 – Complete removal of ACL from a file

Additionally, you can also see that mask is no longer present when checking the ACL with the getfacl command.

# Enhanced access controls

There are additional systems designed to enhance the access controls by implementing security policies. One of the systems is the well-known SELinux.

Linux access controls are determined by a set of policies loaded on the system kernel that enable an improved security mechanism that prevents changes of permissions by careless users or misbehaving applications.