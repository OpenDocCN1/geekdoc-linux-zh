| Options | Descriptions |
| --- | --- |
| option tftp-server-name string; | Indicates the name of the TFTP server that the client should use to transfer the boot image. Used more often with DHCP clients than with BOOTP clients. |
| option bootfile-name string; | Indicates the location of the bootstrap file that is used to boot the client. Used more often with DHCP clients than with BOOTP clients. |
| option x-display-manager ip-address [, ip-address... ]; | Indicates the locations of X Window System Display Manager servers that the client can use, in order of preference. |

# Starting the DHCP server

After the /etc/dhcpd.conf file is configured, you can start the DHCP server immediately. As root user from a Terminal window, type the following:

```
```
# service dhcpd start
```
```

Your DHCP server should now be available to distribute information to the computers on your LAN. If there are client computers on your LAN waiting on your DHCP server, their network interfaces should now be active.

If everything is working properly, you can have your DHCP server start automatically each time your computer boots by turning on the dhcpd service as follows:

```
```
# chkconfig dhcpd on
```
```

There are a few ways you can verify that your DHCP server is working:

+   * Check the /var/log/messages file. If the DHCP service has trouble starting, you will see messages in this file indicating what the problem is.
+   * Check the /var/lib/dhcpd/dhcpd.leases file. If a client has been assigned addresses successfully from the DHCP server, a lease line should appear in that file. There should be one set of information that looks like the following for each client that has leased an IP address:

```
```
lease 10.0.0.225 {
	starts 2 2006/05/04 03:48:12;
	ends 2 2006/05/04 15:48:12;
	hardware ethernet 00:50:ba:d8:03:9e;
	client-hostname "pine";
}
```
```

+   * Launch Wireshark (type wireshark& from a Terminal window) and start capturing data (in promiscuous mode). Restart the DHCP server and restart the network interface on the