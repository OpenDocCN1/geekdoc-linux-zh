Here, it is demonstrated on host s1ug that broadcasts were indeed being received over the Ethernet link between these two hosts. The values are different in this output because it was captured much later than the earlier session shown. However, if you were to establish clients that ran on the local and remote hosts at the same time, you would be able to verify that their content was in full agreement.

# ## Troubleshooting Hints

If you fail to achieve similar results on your own personal network, then a large number of things could be involved in the problem. It is not the intention of this book to describe aspects of network administration or design. Nor will this book be a treatise on network troubleshooting. The following simple tips are offered in the hope that it might prove to be useful as a starting point in diagnosis.

If the problem exists over a simple network of your own construction and there is little or no network traffic on it, you might be able to just look at the hub. Many mini-hubs, for example, offer LED indicators that provide indication of packet traffic for the corresponding ports involved. The server program presented should cause a flicker to occur approximately every four seconds when a broadcast occurs. Failure to see this suggests that the broadcast is not occurring.

Another approach is to use the tcpcdump command, which is now part of most Linux distributions today. An example of tcpdump(8) output is shown as follows while the server was broadcasting:

```
```
s1ug
# tcpcdump udp port 9097
tcpcdump: listening on eth0
21:04:43.987482 pepper.ve3wqw.org.1032 > 192.168.0.255.9097: udp 96
21:04:47.977482 pepper.ve3wqw.org.1032 > 192.168.0.255.9097: udp 96
21:04:51.987482 pepper.ve3wqw.org.1032 > 192.168.0.255.9097: udp 96
```

OUTPUT
```

The command-line arguments used cause only the UDP packets on port 9097 to be displayed. The sample output includes three packet summaries that were displayed. More information about tcpdump(8) can be accessed by reading its manual page.

These are but two very simple methods of checking for broadcast packets. Frequently, however, these simple techniques will be sufficient for the programmer.