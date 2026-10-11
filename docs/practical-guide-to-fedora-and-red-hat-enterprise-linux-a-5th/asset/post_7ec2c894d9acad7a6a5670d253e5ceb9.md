
5. Give the command `/sbin/service network start` to bring up the network interfaces.
6. Start the `named` daemon using `service` as explained in the “Prerequisites” section (page 785). Refer to “Troubleshooting” on page 805 for ways to check that the DNS cache is working.

Once `named` is running, you can see the effect of the cache by using `dig` to look up the IP address of www.sobel1.com, a remote system:

```
$ dig www.sobel1.com

;; <<> DiG 9.6.1-P1-RedHat-9.6.1-11. P1.fc12 <>> www.sobel1.com
;; global options: +cmd
;; Got answer:
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 45364
; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 2, ADDITIONAL: 1

;
; QUESTION SECTION:
;www.sobel1.com.                 IN    A

;
; ANSWER SECTION:
www.sobel1.com.            3600  IN    A    64.13.141.21

;
; AUTHORITY SECTION:
sobel1.com.              3600  IN    NS    ns2.meer.net.
sobel1.com.              3600  IN    NS    ns.meer.net.

;
; ADDITIONAL SECTION:
ns2.meer.net.            172800  IN    A    64.13.153.254

;; Query time: 266 msec
; SERVER: 127.0.0.1#53(127.0.0.1)
;; WHEN: Tue Nov 24 11:20:47 2009
;; MSG SIZE  rcvd: 107
```

The fourth line from the bottom shows that the query took 226 milliseconds (about one-quarter of a second). When you run the same query again, it runs more quickly because the DNS cache has saved the information in memory:

```
$ dig www.sobel1.com
...
; Query time: 5 msec
; SERVER: 127.0.0.1#53(127.0.0.1)
; WHEN: Tue Nov 24 11:21:09 2009
; MSG SIZE  rcvd: 123
```

## When you turn off the DNS cache

> Remember to remove the **PEERDNS** line you added in step 2 if you want to turn off the DNS cache. Under RHEL you must also remove the `caching-nameserver` package.

## JumpStart II: Setting Up a Domain Using system-config-bind

To display the BIND Configuration GUI window (Figure 24-6), enter **system-config-bind** on a command line or select **Main** menu: Applications \* System Tools \* Domain Name System (*Fedora*) or **Main** menu: System \* Administration \* Server Settings \* Domain Name System (*RHEL*).

### Notes

If */etc/named.conf* does not exist, **system-config-bind** displays a dialog box that informs you that it is installing a default configuration. Click **OK**.

The */etc/named.caching-nameserver.conf* file, which is installed as a dependency with the *RHEL* **caching-nameserver** package, is not recognized by **system-config-bind** as a **named** configuration file. See “named.conf” on page 786 for more information about this file.

Each zone file that **system-config-bind** creates has a filename extension of **.db**.

Because the windows displayed by **system-config-bind** contain a lot of information, you may find it helpful to expand or maximize these windows so you can view the information more easily.

![](img/f28adb66a7398a382f0505e0ba74a872_829_0.png)

![](img/f28adb66a7398a382f0505e0ba74a872_830_0.png)

Figure 24-7 The BIND Configuration GUI window with a right-click menu

## Using this JumpStart

> The system-config-bind utility is a complex tool that you may find helpful for setting up BIND. Run this utility and click Help→Manual on the menubar to display the Fedora/RHEL manual for this utility. Click Help→ISC ARM to display the BIND 9 Administrator Reference Manual. You may want to experiment with this utility after you have set up one of the servers described at the end of this chapter, as its configuration information may make more sense after you go through the process of manually configuring BIND.

This section explains how to use system-config-bind but does not go into detail about what each of the files and settings does. That information is covered in other sections of this chapter.

### Using the BIND Configuration GUI Window

Right-click on an object (line) in the BIND Configuration GUI window to display a pop-up context menu. This menu always has an Edit selection, which displays a window in which you can edit information pertaining to the object you clicked. You can display the same window by double-clicking the object or by highlighting the object and clicking Properties on the toolbar. This pop-up menu also always has an Add selection that displays a submenu with choices appropriate to the object you are working with. Figure 24-7 shows the pop-up menu for the DNS Server object, along with the Add submenu.

In the BIND Configuration GUI window, a triangle at the left end of a line indicates that the object holds other objects. Click a triangle so that it points down to expand an entry. Click it so that it points to the right to collapse an entry.

![](img/f28adb66a7398a382f0505e0ba74a872_831_0.png)

Figure 24-8 The first New Zone window

## Setting Up a Domain Server

Highlight **DNS Server** in the BIND Configuration GUI window and click **New Zone** on the toolbar (or right-click and select **Add Zone**) to add a new zone (page 776) and its associated nameserver. In response, system-config-bind displays the first New Zone window (Figure 24-8), which allows you to specify information about the zone you are setting up.

With the drop-down list labeled **Class** displaying **IN Internet**, click **OK** under this list.

Select the origin type from the drop-down list labeled **Origin Type**. The most common choices are **Forward** or **IPv4 Reverse**. Click **OK**. If you selected a forward zone, the **Forward Zone** **Origin** text box replaces the origin type information. Enter the domain name of the zone, including a trailing period, in the text box.

Select the type of zone you want to set up from the drop-down list labeled **Zone Type**. You can select from **master**, **slave**, **forward**, **hint**, and other types of zones. Refer to “Servers” on page 778 and **type** on page 796 for information on types of zones.

After you make your selections and click **OK**, system-config-bind displays the second New Zone window (Figure 24-9, next page). This window enables you to set up SOA information for the zone. Refer to “SOA” on page 781 for information about the fields in the SOA record, including the serial number and the various times (refresh intervals). In this window, the authoritative (primary) nameserver (page 778) defaults to the local system and the email address of the person responsible for the zone defaults to **root** on the local system. If you enter names that do not end with a period in these text boxes, system-config-bind appends the domain name of the zone to the names you have entered. Change the values in this window as necessary. By default, all zone files that system-config-bind creates have the **.db** file-name extension. The default filename for the zone file is the name of the domain you are setting up with an extension of **.db**. Click **OK**.

![](img/f28adb66a7398a382f0505e0ba74a872_832_0.png)

**Figure 24-9** The second New Zone window

After you add a new zone, information about this zone appears in the BIND Configuration GUI window (Figure 24-6, page 789). Click **Save** on the toolbar to save the changes you made before you close the window.

To view information about the new zone, you can expand the object that holds the name of the new zone. You can further expand the Zone Authority Information and Name Server objects that appear when you expand the new zone object. Right-click any object to add to or modify the information in the object or to delete the object.

## Adding Resource Records

You can add any of an extensive list of resource records to a domain. Right-click the object representing the domain you just added to display a pop-up menu. Slide the mouse pointer over **Add** to display the domain **Add** menu (Figure 24-10). The uppercase letters at the left end of each selection specify the type of resource record (page 779) that the selection adds to the domain. Following are some of the choices available on this menu:

- A\tIPv4 Address record (page 780)
- CNAME\tAlias record (page 780)
- MX\tMail Exchange record (page 780)
- NS\tNameserver record (page 780)
- TXT\tText record (page 782)

To add a reverse zone (a PTR record; page 781), add a new zone as before, but this time select IPv4 (or IPv6) Reverse as the origin type. For more information refer to “Reverse Name Resolution” on page 783.

Click Save when you are done, close the BIND Configuration GUI window, and start the named daemon as explained on page 785.

## Setting Up BIND

This section discusses the /etc/named.conf file, zone files, implementation of a DNS cache, and running DNS inside a chroot jail.

![](img/f28adb66a7398a382f0505e0ba74a872_833_0.png)

Figure 24-10\tThe domain Add drop-down menu
