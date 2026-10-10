The primary function of Wireshark is to take a snapshot of the packets coming across your network interfaces and display that data in the Wireshark window. You can filter the data based on a variety of filter primitives. When the capture is done, you can step through and sort the data based on the values in different columns. Optionally, you can save the captured data to a file to study the data at a later time.

> **TIP:** If you can't use Wireshark because you don't have a GUI available, you can use the `tcpdump` command from the shell. It is not as friendly as Wireshark, but it supports the same filtering syntax. Because `tcpdump` can produce a lot of output, you will probably want to use some form of filtering or direct the output of the command to a file. (Type **man tcpdump** for information on filter options.)

# Capturing Ethernet data

With the Wireshark window displayed, you can capture data relating to packet activities on any of your Ethernet network interfaces by doing the following:

+   1. Click **Capture \(\to\) Interfaces**. You will see a list of network interfaces available on your computer.
+   2. Click **Options** next to the interface you want to capture from (probably **eth0** for a wired Internet or **wlan0** for a wireless interface). A Wireshark **Capture Options** window appears.
+   3. Choose options relating to what data is captured:

+   *   **Capture packets in promiscuous mode** — Any computer on a LAN can see all packets that traverse the LAN, except those packets intended for switched portions of the LAN. With this on, all packets seen by your network interface are captured. With this mode off, only packets intended specifically for your network interface (including multicast and broadcast packets) are captured. In other words, turn on promiscuous mode to monitor the whole LAN and turn it off to monitor only your interface.
+   *   **Limit each packet to** — Limits the size of each packet to a maximum number of bytes.
+   *   **Capture Filter** — This optional field lets you enter a filter that can be used to filter capture data. You can type in filters individually or click the **Filter** button to use a filter you have stored earlier.

> **CROSS-REFERENCE:** Filtering is one of the most powerful features of Wireshark. See the sidebar “Using Wireshark Filters” for further information on how to enter filters into the Filter field.

+   *   **Capture file(s)** — Enter the name of a file in which you want to capture the data gathered. If you don't enter a filename, the information will be displayed on the Wireshark window without being saved to a file.
+   *   **Ring buffer (Number of files)** — Select this option to have packets captured in a set number of files. To use this feature, you must also specify a filename (such as