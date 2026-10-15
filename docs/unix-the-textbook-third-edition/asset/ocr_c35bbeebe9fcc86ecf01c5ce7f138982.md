# Section 23.9. But that is not the only reason an ordinary user or system administrator would deploy the virtualization methods we demonstrate.

A user might want to take advantage of some of the facilities that an additional OS offers, above and beyond what is available as the main OS into which the computer boots. Instead of shutting down the main OS, and then booting into the additional OS, both can be run simultaneously using the virtualization method shown here. For example, Solaris does not offer LibreOffice as an application, but PC-BSD does by default. So if you run both OSs simultaneously, you can use LibreOffice and Solaris applications and facilities on the same machine. Of course, there are trade-offs in doing this, mainly in terms of performance speed and disk usage.

Also advantageous is the deployment of VMs to allow you to “test drive” a particular OS without devoting an entire hardware platform to it. This can also be achieved by running a “live” version of it from a DVD or a USB thumb drive, but the performance speed and persistence of data using these techniques is somewhat limited. In this chapter, we show several examples of installing guest VMs on mainstream OSs, such as LINUX and Windows, to allow you to “test drive” our base UNIX systems in a more fully functional way.

# 25.1.1 Virtualized Network Addresses in PC-BSD and Solaris

In the examples shown in the next sections, it is necessary to have the VM guest system network connection “bridged” to the host system. We show how to do this in Example 25.8, but as a preliminary consideration, you need to be able to quickly discover what the network address of a PC-BSD or Solaris machine is. That is true whether you are running either of those systems as a stand-alone, or inside of a VM environment. We also detail the commands we use here in Section 23.8.3, “Network Configuration.”

For Solaris, you use the ipadm show-addr command, and on PC-BSD you use the ifconfig command, as follows:

```
On Solaris:
bob@solaris113beta:~$ dladm show-link
LINK        CLASS     MTU    STATE    OVER
net0        phys      1500   up       --
bob@solaris113beta:~$ ipadm show-addr
ADDR_OBJ    TYPE      STATE      ADDR
lo0/v4      static    ok         127.0.0.1/8
net0/v4     dhcp      ok         192.168.0.15/24
lo0/v6      static    ok         ::1/128
net0/v6     addrconf  ok         fe80::a00:27ff:febb:de8e/10
bob@solaris113beta:~$
```

The Internet Protocol (IP) address of this Solaris machine, as shown in bold type in the ipadm command output, is 192.168.0.15

On PC-BSD:
[bob@pcbsd-1233] ~% ifconfig