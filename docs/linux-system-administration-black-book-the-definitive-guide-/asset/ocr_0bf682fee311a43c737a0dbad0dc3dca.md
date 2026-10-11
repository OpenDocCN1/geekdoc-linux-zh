**Table 18.1 Methods of specifying hosts in /etc/smb.conf.**

| Format | Description | Example |
| :--- | :--- | :--- |
| host | Specifies the name of the machine you are referring to | blue |
| hostIP | Specifies the IP address for the machine you are referring to | 192.168.160.5 |
| networkIP | Specifies an entire network of machines using a wildcard format | 192.168.160 |
| IPrange | Specifies a range of IP addresses | 192.168.160.0/255.255.255.110 |

After setting what hosts are allowed, the file has the following statements:

```
printcap name = /etc/printcap
load printers = yes
```

The **printcap name** statement sets the file that Samba looks to when it needs to access printers. On the other hand, the **load printers** statement is more basic. If you answer **yes** here, then all printers in the file specified in the preceding line are loaded for use by Samba-connected machines. An answer of **no** refuses access to the printers over SMB.

After the basic printer issues are dealt with, you can ignore the following line:

```
; printing = bsd
```

The **printing** statement determines how Samba tries to talk to the printers. Possible print system types—whether specific to a particular Unix flavor or independent of flavor—are listed in Table 18.2. Although the types defined in the table are uppercased because they are typically acronyms, they should be lowercased with the **printing** statement.

After the **printing** statement is more commented-out code:

```
; guest account = pcguest
```

The **guest account** statement enables you to specify what username is assigned to guest logins, if they are activated for the service the user is trying to access. When this line is commented out, as you see now, guest accesses are assigned to the **nobody** account. After deciding on guest access, you reach the following:

```
log file = /var/log/samba/log.%m
```

![](bbox=[0.92, 0.76, 0.97, 0.94])