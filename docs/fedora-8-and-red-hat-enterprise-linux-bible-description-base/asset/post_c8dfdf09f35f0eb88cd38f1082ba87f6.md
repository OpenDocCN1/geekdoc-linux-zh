
## Interpreting captured Ethernet data

With the captured data displayed in your Wireshark window, you can get a detailed view of the network traffic that your computer is exposed to. The Wireshark window is divided into three parts. The top part contains a scrollable list of packets. The protocol tree for the current packet appears in the middle part of the display. A hexadecimal dump of the entire contents of the packet appears in the bottom part.

You can sort data in different ways from the top part of the window by clicking the column headings. To see more details related to different items in the protocol tree for the current packet, you can click the triangle-shaped icon next to the protocol information that interests you.

The following tips will help you interpret what the data means:

- The **Source** and **Destination** columns show where each packet came from and where it went. If the **Enable name resolution** option is on (which is recommended), the hostname associated with IP packets is displayed. This makes it much easier to see which computer is communicating with you.
- To see all activity associated with a particular location, click the **Source** or **Destination** column. Packets will be sorted alphabetically, making it easier for you to scroll through the activity list for the location that interests you.
- If you are trying to debug a particular feature, click the Protocol column to gather activities based on protocol. For example, if you were trying to get Samba to work (for Windows file or printer sharing), sorting by protocol would enable you to see all NetBIOS and NBNS (NetBIOS name server) requests that came to your computer.
- To mark a packet of interest to you, click the middle mouse button. This will highlight the packet, making it easier to find later. (If you have only a two-button mouse, and you indicated during installation that it should emulate a three-button mouse, you can click both mouse buttons together to emulate the middle mouse button.)

### Using Wireshark Filters

If you are monitoring a busy server or a busy network, Wireshark can gather so much data that it can become almost unusable. If you know what you are looking for, however, you can filter what packets are captured based on values you enter.

Filters in Wireshark are implemented using the pcap library (type `man pcap` to read about it). The filter expressions you can use with Wireshark are described on the `tcpdump` man page. Here are some examples of filters that you could enter into the Filter box when you capture Ethernet data with Wireshark:

```
host 10.0.0.15
```

The `host` primitive lets you capture only packets that are either to or from a particular host computer (by IP address or hostname). By preceding `host` with `src` or `dst`, you can indicate that you only want packets sent from a particular source or to a particular destination host.

```
tcp port 80
```

You can enter a protocol name (such as `tcp`, `ether`, `udp`, or `ip`) to limit captured packets to those that are assigned to that protocol. As shown in the previous example, with `tcp` you could also indicate a port number (such as 80, to monitor traffic to and from your Web server).

You can filter for certain special activities on the network, using the `gateway`, `broadcast`, or `multicast` primitives. Entering `gateway host` lets you find packets sent to a gateway host that is neither a Source nor Destination for the packet (which is determined because the Ethernet address doesn't match either of those IP addresses). Enter `ether broadcast` to monitor broadcast packets on your Ethernet network, such as announcements from name servers announcing availability. Likewise, you could filter for multicast packets on ether or `ip` protocols (`ether multicast`).

---

1. Click **Capture** → **Interfaces**. You will see a list of network interfaces available on your computer.
2. Click **Prepare** next to the interface you want to capture from (probably `eth0` for a wired Internet or `wlan0` for a wireless interface). A Wireshark Capture Options window appears.
3. Choose options relating to what data is captured:
   - **Limit each packet to:** Limits the size of each packet to a maximum number of bytes.
   - **Capture packets in promiscuous mode:** Any computer on a LAN can see all packets that traverse the LAN, except those packets intended for switched portions of the LAN. With this on, all packets seen by your network interface are captured. In other words, turn on promiscuous mode to monitor the whole LAN and turn it off to monitor only your interface.
   - **Capture Filter:** This optional field lets you enter a filter that can be used to filter capture data. You can type in filters individually or click the Filter button to use a filter you have stored earlier.
     > **CROSS-REFERENCE:** Filtering is one of the most powerful features of Wireshark. See the sidebar “Using Wireshark Filters” for further information on how to enter filters into the Filter field.
   - **Capture file(s):** Enter the name of a file in which you want to capture the data gathered. If you don’t enter a filename, the information will be displayed on the Wireshark window without being saved to a file.
   - **Ring buffer (Number of files):** Select this option to have packets captured in a set number of files. To use this feature, you must also specify a filename (such as `/tmp/abc`) and a file size. Data will be put into files you choose, named from the root filename you have provided. Once the files fill up, Wireshark will go back and write to the first file again and continue filling up the files. When you stop the capture, you are left with the number of capture files you chose, containing the most recent data.
   - **Update list of packets in real time:** Select this option to have packet information appear in the Wireshark window as each packet crosses the interface. With this option off, the information is displayed after you stop capturing it.
   - **Automatic scrolling in live capture:** If you are updating packets in real time, select this option to have packet information scroll up after the screen fills. With this off, you just see the first screen of packets and have to scroll down manually to see the rest.
   - **Hide Capture info dialog:** Prevents the Capture Info box from appearing to display the number and types of packets being captured.
   - **Stop Capture after \_. \_. \_.:** By default, Wireshark will capture data from the moment you click OK until you click Stop (with this value set to 0). Or, select one of the three Stop Capture fields and type a number to capture only that number of packets; a number to stop capture after a set number of bytes, kilobytes, megabytes, or gigabytes of data; or a number to indicate the number of seconds, minutes, hours or days to capture data. When the limit is reached, capture stops and the file is stored in `/tmp/etherXXXX???????`, where `???????` is replaced by a string of characters.
   - **Enable MAC/network/transport name resolution:** With any of these three options on, names are displayed instead of addresses (if possible). For example, for transport names, Source and Destination IP addresses are displayed as hostnames (if they can be resolved from `/etc/hosts` or DNS). With this option off, IP addresses appear in the Source and Destination columns.
4. Click **Capture**. Wireshark begins gathering data on packets encountered by the interface. The Wireshark Capture window displays information on how many incoming and outgoing packets have crossed the interface since the capture began. The number of packets that are associated with each protocol Wireshark monitors is displayed, along with the percentage of total packets associated with each protocol.
5. Click **Stop** (or the capture might stop automatically, if it has reached a size or time limit set by you). The snapshot of data you just took will appear on the Wireshark window. Packets are displayed in the order in which they traversed the interface.
6. You can choose to save the data to your hard disk by selecting **File → Save As**.

At this point, you can start interpreting the data.
