
## Nmap Scan Results

| Port | State | Protocol | Service |
|------|-------|----------|---------|
| 23   | open  | tcp      | telnet  |
| 79   | open  | tcp      | finger  |
| 6001 | open  | tcp      | X11:1   |

TCP Sequence Prediction: Class=random positive increments  
Difficulty=659 (Medium)

Remote operating system guess: IOS Version 10.3(15) - 11.1(20)

Nmap run completed -- 1 IP address (1 host up) scanned in 4 seconds

## Xtraceroute Tool

The xtraceroute tool is an X Window application based on its command-line counterpart, traceroute. It provides a GUI interface and features a rotating globe showing the path of an xtraceroute session. Recall that the traceroute command, described in the previous chapter, uses the Internet Protocol to record each destination or hop en route to a specific target host. The command-line version records each hop by displaying the IP address and general performance information. This version of the tool provides the same information but also displays hops on a three-dimensional globe that can be moved with the mouse to control the viewing angle.

The xtraceroute software maintains a database that contains destination information such as IP and hostname. It also contains latitude and longitude information so that, should xtraceroute visit that site, it may be displayed on the globe. The user also has the ability to enter additional destinations not already provided in the standard database.

Figure 5.20 shows what will be displayed when xtraceroute is used to trace the path from the East Coast (Orlando, FL) of the USA to the xtraceroute Web site that is located on the West Coast of Sweden. Note that a line is drawn from Florida over the Atlantic and to Europe.

The tool's main window contains two menus, two panels, and two buttons. The first menu, File, has two items: New... and Quit. The Info button displays specific information on the host entry. The other button, which is blank, is located on the main window and is a shortcut to the New... submenu. The New... submenu item is used to enter a destination target. To determine the correct path, xtraceroute will use the destination addresses entered by the user. Selecting this submenu will display the dialog window shown in Figure 5.21. The user can enter either a fully qualified hostname or valid IP address. In the window shown in Figure 5.21, the Internet host location of where the xtraceroute software is available was entered.

The other submenu item is Quit, which is self-explanatory. The other menu item, Database, contains three submenu items. Each of these items accomplishes the same basic task—to add additional destination information so that xtraceroute can display the site on the globe. The most useful of the three is the Add Host... submenu item. Selecting this option will display the dialog box shown in Figure 5.22.

Clicking the Help button in this dialog box will provide additional information about adding global coordinates for the host entry being added.

When xtraceroute was first installed, the database didn't contain any information regarding the networks that covered the Orlando area. As a result, host information was added manually to the xtraceroute database. Some of this information is dependent on the user's Internet location. The user will use the New host record window to add new entries to the database. In Figure 5.22, the entry point for the Internet starts with a local ISP with the hostname of `1.orlando-11-12rs.fldial.access.att.net` and an IP address of `12.77.196.1`, which were entered in the Hostname and IP number fields, respectively. The Latitude and Longitude fields include the global coordinates of the location as shown on a world map or globe. Please keep in mind that both the latitude and longitude numbers were approximated for this example. Finally, the location including the city and state was entered into the Info field.

Clicking the **Ok** button will add this entry to a local file called `user_hosts.cache`, which is stored in subdirectory `.x` in the user's home directory. Unfortunately, the `.x` directory must be manually created before xtraceroute will save any files to this location. This file is read when xtraceroute starts up and xtraceroute uses this database when updating the three-dimensional globe panel.

Like regular `traceroute`, the hop count, and hop hostname/IP are displayed in the bottom panel of the main window. Unlike normal `traceroute`, xtraceroute doesn't provide network round-trip performance information in the main panel. Instead, the user must select a hop destination and click the *Info* button located on the bottom of the main panel to get trip time data. Clicking this button displays a new window, as depicted in Figure 5.23.

This window contains a few fields not shown in the window shown in Figure 5.22. These new fields include the *Ping time*, *Minimum distance*, and *Accuracy* fields. The *Ping time* field represents the round-trip time delay in microseconds for the originating site, and in this case, the destination target happens to be `palver.dtek.chalmers.se`. This particular host is located at the Chalmers University of Technology. The *Minimum distance* field helps define the length of the path to the remote destination. The final field, Accuracy, provides helpful information about the source of the destination information. The window also contains two buttons that make it easier to navigate the hops within the main window. The Next button moves closer to the destination target, while the Prev button moves further away from the destination target but closer to the source of the trace.

One of the powerful features of xtraceroute is its ability to manipulate the three-dimensional globe using the mouse. By default, when the application is first started, the entire continent of Africa is in view, with parts of Europe toward the top, and South America on the left. When a destination is entered and xtraceroute begins, it draws a starting point indicating the origin of the trace and one or more lines indicating each hop along the route to the final destination. Depending on which continent the user issues the trace from, the destination connecting point may not be in view. In this situation, use the mouse to bring the lines into view once the trace is complete. Use the left mouse button to drag the globe to the location desired. Sometimes, if the user holds the mouse tool long or if the globe is dragged too far, the desired position is skipped. In time and with a little practice, controlling the position of the continents will be easy.

As previously mentioned, the xtraceroute database may not contain either the site where the user is located, any destination along the path of the target, or the target itself. As a result, the user must enter this information manually. Instead of using the GUI, the user may manually add entries to the default database located in his home directory. For instance, Listing 5.2 shows a few entries that were used to provide the path between the East Coast of the USA and West Coast of Sweden.

### Listing 5.2 User's personal database for xtraceroute

| Entry | IP Address | Hostname | Lat Deg | Lat Min | Lat Sec | Lat Dir | Lon Deg | Lon Min | Lon Sec | Lon Dir |
|-------|------------|----------|---------|---------|---------|---------|---------|---------|---------|---------|
| 1 | 199.70.195.54 | 199.70.195.54 | 30 | 0 | 0 | n | 81 | 0 | 0 | w |
| 2 | 12.77.196.1 | 1.orlando-11-12rs.fldial.access.att.net | 30 | 0 | 81 | 0 | 0 | w | | |
| 3 | 12.127.9.101 | br3-p390.wswdc.lp.att.net | 23 | 33 | 16 | n | 81 | 33 | 18 | w |
| 4 | 204.70.10.150 | core5-hss15-0-0.Washington.cw.net | 38 | 30 | 0 | n | 27 | 5 | 59 | w |

The format of the personal database includes the IP address and hostname of the destination, followed by standard global coordinates. The interpretations of the coordinates included in the first entry are 30 degrees, zero minutes, zero seconds north of the equator or by 81 degrees, zero minutes, zero seconds in the western hemisphere. When each hop destination is added to this file, **xtraceroute** will display a much more accurate mapping between the source of the trace and the final destination.
