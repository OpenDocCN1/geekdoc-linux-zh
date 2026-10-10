
## Customizing the Network List Window

As we have seen, Kismet’s main display contains a significant amount of useful information in the network list section. All of the information for a particular network is available in the network details window. Any or all of this information can be displayed in the main window by modifying the `kismet_ui.conf` file. The recognized columns, and their appropriate descriptions, are as follows (default columns are **bold**):

- bssid: BSSID (MAC address) of the network
- **channel**: Last-advertised channel for network
- **clients**: Number of clients (unique MACs) seen on network
- crypt: Number of encrypted packets
- **data**: Number of data packets
- decay: Displays ‘/’ or ‘.’ or blank, based on network activity in the last ‘decay’ seconds (controlled by the ‘decay’ variable in the config file)
- **duplicate**: Number of packets with duplicate IVs seen
- flags: Network status flags (Address size, decrypted, etc)
- info: Extra AP info included by some manufacturers
- **ip**: Detected/guessed IP of the network
- llc: Number of LLC packets
- manuf: Manufacturer, if matched
- maxrate: Maximum supported rate as advertised by AP
- **name**: Name of the network or group
- noise: Last seen noise level
- **packets**: Total number of packets
- shortname: Shortened name of the network or group for small displays
- shortssid: Shortened SSID for small displays
- **signal**: Last seen signal level
- signalbar: Graphical representation of signal strength
- snrbar: Graphical representation of signal-to-noise ratio
- **size**: Amount of data transferred on network
- ssid: SSID/ESSID of the network or group
- **type**: Network type (Probe, Adhoc, Infra, etc)
- **weak**: Number of packets which appear to have weak IVs
- **wep**: WEP status (does network indicate it uses WEP)

To modify the default columns in the main window, edit the `kismet_ui.conf` file at the following location:

```
# What columns do we display? Comma separated.  Read the documentation for what
# columns are valid.
columns=decay,name,type,wep,channel,packets,flags,ip,size
```

Figure 4.18 shows a modified network list panel showing network name, manufacturer, total number of data packets by network, signal and noise information, and amount of data transferred per network.

### Figure 4.18 Modified Network List Window

![](img/d6ac176c353d2b7687c1186a140180a1_113_0.png)

## Customizing the Client List Window

Similarly, the columns in the client window can be modified (all are on by default except “maxrate”):

| Column | Description |
| :--- | :--- |
| (implied context from previous page, likely "data" or similar) | Number of encrypted data packets transferred by client |
| noise | Last seen noise level of client |
| signal | Last seen signal level of client |
| size | Amount of data transferred by client |
| type | Type of client (Established, To-DS, From-DS, etc) |
| weak | Number of packets which appear to have weak IVs |

To modify the default columns in the client window, edit the *kismet_ui.conf* file at the following location:

```
# What columns do we display for clients? Comma separated.
clientcolumns=decay,type,mac,manuf,data,crypt,size,ip,signal,quality,noise
```

## Customizing Colors

Kismet's colors can be turned on or off, the background and border colors can be changed, and the default colors listed above can be changed by modifying the applicable portion of *kismet_ui.conf*:

```
# Colors (front, back) of text in the panel front. Valid colors are:
# black, red, yellow, green, blue, magenta, cyan, white
# optionally prefixed with "hi-" for bold/bright colors, ie
# hi-red, hi-yellow, hi-green, etc.
# Enable colors?
color=true
# Background
backgroundcolor=black
# Default text
textcolor=white
# Window borders
bordercolor=green
# Titles
titlecolor=hi-white
# GPS and APM info
monitorcolor=hi-white
# WEP network color
wepcolor=hi-green
# Factory network color
factorycolor=hi-red
# Open color
opencolor=hi-yellow
# Cloaked network color
cloakcolor=hi-blue
```

## Third Party Front-ends

While the large majority of this chapter has focused on Kismet’s native panels interface, there are a number of third-party interfaces that have been developed over the years. These third-party front-ends are designed primarily as a way of enhancing the look or changing the interface from an ncurses/panel one to a truly graphical one. This section is not meant to be an exhaustive review of such graphical user interfaces (GUIs), but rather a brief survey of some of the options that are available.

> NOTE  
> It is important to note that these third-party front-ends are simply replacements for the Kismet client (interface), and don’t actually do anything by themselves. They still require you to run Kismet in server mode and connect to it with the particular interface of your choice.

### gkismet

One example of a popular Linux-based Kismet front end is gkismet (see Figure 4.19). The gkismet interface is designed to supplement or replace the native Kismet panels interface for those that prefer something more GUI-based. Many of the same features are available, and development is ongoing to remain compatible with the latest version of Kismet. For more information about gkismet, see http://gkismet.sourceforge.net/.

### Figure 4.19 gkismet

![](img/d6ac176c353d2b7687c1186a140180a1_116_0.png)

### KisWin

*KisWin* (not to be confused with RenderMan's Kismet for Windows package also known as KisWin, and located at [http://www.renderlab.net/projects/wrt54g/](http://www.renderlab.net/projects/wrt54g/)) is a Windows-based GUI front-end for Kismet (see Figure 4.20). Whether you are running Kismet on Windows/Cygwin using a remote drone (such as a modified Linksys WRT54G), using CACE Technologies' AirPcap adapter, or simply running Kismet over a network to a Windows PC, KisWin provides you with a GUI interface.
For more information about KisWin, see http://kiswin.taz00.com/

### Figure 4.20 KisWin

![](img/d6ac176c353d2b7687c1186a140180a1_117_0.png)

### dumb kismet client

The last interface we'll mention is dumb kismet client for Win32. This particular client is lightweight, and should be able to run in front of any of the same Windows/Cygwin configurations as KisWin. While dkc is designed for Windows, it also worked fine under Linux using wine. For information about dumb kismet client, see http://www.d3tr.de/dkc/.

### Figure 4.21 dumb kismet client

![](img/d6ac176c353d2b7687c1186a140180a1_118_0.png)

### Further information

Once again, this section is not designed to be the end-all solution for third-party front-ends for Kismet, rather a sampling of some of the solutions that are available to users. See http://www.kismetwireless.net/links.shtml for more information on third-party tools for Kismet.

## Summary

The Kismet client is the primary interface between the Kismet server and the user. The default display is the panels interface, which is a lightweight, interactive GUI display. The primary display provides the user with a general overview of Kismet’s collected data, and can be manipulated and modified to the user’s content. The remainder of the windows are secondary displays or pop-up windows that provide additional and amplifying information about selected networks, groups, or clients, as well as statistics and additional interesting information. Some of these displays can also be modified to the user’s liking. Lastly, there are a number of third-party front-ends to supplement or replace the default Kismet client.

What happens when you have a question? Your first source of information should be Kismet itself. Most if not all of the displays have integrated help screens (always the **h** key). Your second source should be the online documentation, found at www.kismetwireless.net/documentation.shtml. Of particular interest to this chapter are sections 10 (NCurses/panel interface), 17 (Troubleshooting), and 18 (Frequently Asked Questions). You would benefit greatly from reading the documentation in its entirety (all the way to the end!). Once you exhaust those sources, move on to the Kismet forums (http://www.kismetwireless.net/forum.php), being sure to search before you post. Finally, consider using your best friend Google who, more often than not, can find something that will guide you in the right direction.

## Solutions Fast Track

### Main Display

- The Kismet panels display is the primary interface between the Kismet client and server and the user.
- The main display is divided into the network list panel, status panel, and information panel; and is designed to provide the user with an overview of Kismet’s collected information.
- Kismet’s integrated help feature is the gateway to more detailed information about a particular network.
