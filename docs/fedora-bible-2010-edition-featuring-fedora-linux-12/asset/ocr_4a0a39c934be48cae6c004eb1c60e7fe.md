*/tmp/abc*) and a file size. Data will be put into files you chose, named from the root filename you have provided. Once the files fill up, Wireshark will go back and write to the first file again and continue filling up the files. When you stop the capture, you are left with the number of capture files you chose, containing the most recent data.

+   - **Update list of packets in real time** — Select this option to have packet information appear in the Wireshark window as each packet crosses the interface. With this option off, the information is displayed after you stop capturing it.

+   - **Automatic scrolling in live capture** — If you are updating packets in real time, select this option to have packet information scroll up after the screen fills. With this off, you just see the first screen of packets and have to scroll down manually to see the rest.

+   - **Hide capture info dialog** — Prevents the Capture Info box from appearing to display the number and types of packets being captured.

+   - **Stop Capture after...** — By default, Wireshark will capture data from the moment you click OK until you click Stop (with this value set to 0). Or, select one of the three Stop Capture fields and type a number to capture only that number of packets; a number to stop capture after a set number of bytes, kilobytes, megabytes, or gigabytes of data; or a number to indicate the number of seconds minutes, hours or days to capture data. When the limit is reached, capture stops and the file is stored in /tmp/etherXXXX?\*?\*\*\*\*\*, where ??????\*\* is replaced by a string of characters.

+   - **Enable MAC/network/transport name resolution** — With any of those three options on, names are displayed instead of addresses (if possible). For example, for transport names, Source and Destination IP addresses are displayed as hostnames (if they can be resolved from /etc/hosts or DNS). With this option off, IP addresses appear in the Source and Destination columns.

+   4. Click Start. Wireshark begins gathering data on packets encountered by the interface.

+   5. The Wireshark Capture window displays information on how many incoming and outgoing packets have crossed the interface since the capture began. The number of packets that are associated with each protocol Wireshark monitors is displayed, along with the percentage of total packets associated with each protocol.

+   6. Click Stop (or the capture might stop automatically, if it has reached a size or time limit set by you). The snapshot of data you just took will appear on the Wireshark window. Packets are displayed in the order in which they traversed the interface.

+   7. You can choose to save the data to your hard disk by selecting File \u2192 Save As.

At this point, you can start interpreting the data.

# Interpreting captured Ethernet data

With the captured data displayed in your Wireshark window, you can get a detailed view of the network traffic that your computer is exposed to. The Wireshark window is divided into three parts. The top part contains a scrollable list of packets. The protocol tree for the current