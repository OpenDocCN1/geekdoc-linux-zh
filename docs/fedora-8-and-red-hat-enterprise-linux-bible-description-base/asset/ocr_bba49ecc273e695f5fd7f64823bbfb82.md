gnome packages from the Internet by typing `yum install wireshark wireshark-gnome`, or you can use the `rpm` command to install them from the installation DVD.)

The primary function of Wireshark is to take a snapshot of the packets coming across your network interfaces and display that data in the Wireshark window. You can filter the data based on a variety of filter primitives. When the capture is done, you can step through and sort the data based on the values in different columns. Optionally, you can save the captured data to a file to study the data at a later time.

> TIP: If you can't use Wireshark because you don't have a GUI available, you can use the `tcpdump` command from the shell. It is not as friendly as Wireshark, but it supports the same filtering syntax. Because `tcpdump` can produce a lot of output, you will probably want to use some form of filtering or direct the output of the command to a file. (Type `man tcpdump` for information on filter options.)

![](bbox=[0.13, 0.36, 0.85, 0.74])

# Capturing Ethernet data

With the Wireshark window displayed, you can capture data relating to packet activities on any of your Ethernet network interfaces by doing the following: