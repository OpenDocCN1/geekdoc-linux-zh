|     |      |      |       |
|-----|------|------|-------|
| 23  | open | tcp  | telnet|
| 79  | open | tcp  | finger|
| 6001| open | tcp  | X11:1 |

TCP Sequence Prediction: Class=random positive increments
Difficulty=659 (Medium)

Remote operating system guess: IOS Version 10.3(15) - 11.1(20)

Nmap run completed -- 1 IP address (1 host up) scanned in 4 seconds

# ## Xtracroute Tool

The xtracroute tool is an XWindow application based on its command line counterpart, traceroute. It provides a GUI interface and features a rotating globe showing the path of an xtracroute session. Recall that the traceroute command, described in the previous chapter, uses the Internet Protocol to record each destination or hop en route to a specific target host. The command-line version records each hop by displaying the IP address and general performance information. This version of the tool provides the same information but also displays hops on a three-dimensional globe that can be moved with the mouse to control the viewing angle.

The xtracroute software maintains a database that contains destination information such as IP and hostname. It also contains latitude and longitude information so that, should xtracroute visit that site, it may be displayed on the globe. The user also has the ability to enter additional destinations not already provided in the standard database.

Figure 5.20 shows what will be displayed when xtracroute is used to trace the path from the East Coast (Orlando, FL) of the USA to the xtracroute Web site that is located on the West Coast of Sweden. Note that a line is drawn from Florida over the Atlantic and to Europe.

The tool's main window contains two menus, two panels, and two buttons. The first menu, File, has two items: New... and Quit. The Info button displays specific information on the host entry. The other button, which is blank, is located on the main window and is a short cut to the New... submenu. The New... submenu item is used to enter a destination target. To determine the correct