After you press Enter, you will be asked a series of questions regarding your service. You will need to have your username, password, and an understanding of how you want your system set up. The `rp-pppoe` software will automatically initiate IP *masquerading* or Internet connection sharing for your LAN, along with a firewall if you desire. If you only have a single workstation connected to the DSL modem, at least allow the script to set up firewalling. If your computer is on a LAN, and you wish with other users to be able to share the connection, you will need an additional Ethernet interface for your computer. You will also need to use IP masquerading.

After the service is installed and configured for your system, connecting to the Internet is instantaneous, and as simple as this:

```
# sdsl-start
```

To shut down service, use:

```
# sdsl-stop
```

# Using Netscape Communicator

The premiere free—but commercial—software Web browser for Linux is Netscape Communicator. This section covers the commercial version of Communicator, which is generally included with all Linux distributions (except Debian). A free and open source version, named *mozilla*, is also available for Linux and has steadily matured after Netscape released the source code for the browser nearly two years ago. This move stunned the industry and forced many corporations to rethink Archaic views regarding the Open Source paradigm (similar views, along with Fear, Uncertainty, and Doubt, [FUD], are still being spread by the monopolistic software industry). Many Mac OS users are familiar with Netscape’s software, despite the fact that Apple adopted a less popular product in 1997 after a $150 million cash infusion.

Netscape Communicator is, in fact, several programs embodied in a single client. As you will see in the following sections, Netscape can be used for browsing the Web, electronic mail, and reading Usenet newsgroups.

![](bbox=[0.05, 0.8, 0.14, 0.93])

> YDL 2.0 also includes the Open Source version of Netscape Navigator, known as Mozilla. If you use KDE, choose the Migrate Netscape Profile menu item under the panel’s Internet menu to incorporate your existing Netscape settings for use with Mozilla.