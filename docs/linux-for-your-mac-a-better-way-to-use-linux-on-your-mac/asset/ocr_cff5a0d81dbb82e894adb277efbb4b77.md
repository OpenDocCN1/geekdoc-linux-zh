A simplistic command-line equivalent (limited to a single directory search) for help2conf would use the find, xargs, fgrep and less commands like this:

```
$ find / | xargs fgrep searcbst | less
```

In this example, the find command feeds the xargs' fgrep command a list of filenames. The fgrep command will then only display matching lines containing searcbst, preceded by the file's path. By using the less pager you can then quickly browse through a list of documents that contain the search string.

# # Using netcfg

The netcfg client is a an easy-to-use networking tool that can quickly set up your system's /etc/resolv.conf, /etc/hosts, and networking device initialization scripts to support built-in Ethernet interfaces and PCI or PCMCIA network cards. As with all system administrative tools, this client requires root access. netcfg may be launched by clicking its icon on the panel, or from the command line of an X terminal window like this:

```
# netcfg &
```

After you press Enter, its main dialog box will appear, as shown in Figure 14.7.

This client can be used to create and control PPP, PLIP, SLIP, Ethernet, and a variety of network interfaces for your system. You can also alter your system's routing table to accommodate other subnets, define a gateway, or determine how an interface is assigned an IP (Internet Protocol) address.

![](bbox=[0.06, 0.67, 0.55, 0.95])

Figure 14.7  The netcfg client can be used to quickly define and save a variety of network interfaces for a Red Hat-based Linux system.