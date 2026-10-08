the upcoming sections, I cover some additional commands that I often use.

# arp

**arp** is used to display and edit the Address Resolution Protocol (arp) cache, which maps IP addresses to physical hardware addresses. The cache has in it one or more addresses of recently accessed systems. The following example shows issuing the **arp** command on a Windows system at address 113 and the address of the system most recently accessed at 111, with its physical hardware address shown.

```
d: **arp -a**

```
Interface: 159.260.112.113 on Interface 2

  Internet Address          Physical Address        Type
  159.260.112.111          08-00-09-f0-bc-40       dynamic
```
```

There are several options to the **arp** command that you can view by issuing the **arp /? command**.

# ipconfig

**ipconfig** is used to display the current networking interface parameters. The following example shows issuing the **ipconfig** command on a Windows system at address 113 with the **/all** option set, which shows all information related to the networking interface: