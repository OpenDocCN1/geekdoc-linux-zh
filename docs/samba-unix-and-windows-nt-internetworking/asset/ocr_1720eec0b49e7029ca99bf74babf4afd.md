```
wins server = <IP address or DNS name>
```

Next you will need a system operating as the domain master browser to collect and synchronize the browse lists from the various local master browsers (Figure 9.4). The domain master can be either a Samba server or an NT domain PDC, but not both. Remember that an NT domain PDC is automatically designated as the domain master browser.

![](bbox=[0.14, 0.34, 0.9, 0.76])

Figure 9.4: Domain master browser, multi-subnet configuration

To make Samba the domain master, enable the domain master, local master, and preferred master parameters. Set the os level parameter to '65' to exceed the value of all other systems in the workgroup.

```
domain master = yes
local master = yes
preferred master = yes
os level = 65
```

If you already have a Windows NT PDC serving the domain make certain that Samba's domain master parameter is disabled:

```
domain master = no
```