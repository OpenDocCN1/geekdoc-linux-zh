# 276 Appendix A

`bootdelay`—Wait this many seconds before executing the contents of the `bootcmd` variable. The delay can be interrupted by pressing any key before the `bootcmd` sequence starts.
**Warning:** setting `bootdelay` to 0 executes `bootcmd` immediately, and effectively disables any interaction with u-boot. On the other hand, setting this variable to $-1$ disables auto boot.

`bootfile`—Name of the default image to be loaded by any of the download commands.

`ethaddr`—MAC address for the first or only Ethernet interface on the board, known to Linux as `eth0`. A MAC address is 48 bits, represented as six pairs of hex digits separated by dots.

`eth1addr`, `eth2addr`—MAC addresses for the second and third Ethernet interfaces when present.

`ipaddr`—Set an IP address on the target board for TFTP downloading.

`loadaddr`—Default buffer address in RAM for commands like `tftpboot`, `loads`, and `bootm`. Note: it appears, but does not seem to be documented, that there is a default load address, 0x82000000, built into the code.

`serverip`—IP address of the TFTP or NFS server used by the `tftpboot` and `nfs` commands.

`serial#`—A string containing hardware identification such as type, serial number, etc. This variable can only be set once, often during manufacturing of the board. U-boot refuses to delete or overwrite this variable once it has been set.

`verify`—If set to "n" or "no", disables the checksum calculation over the complete image in the `bootm` command to trade speed for safety in the boot process. The header checksum is still verified.

The following environment variables can be automatically updated by the network boot commands (`bootp`, `dhcp`, or `tftp`) depending on the information provided by your boot server:

+   * `bootfile`—See above
+   * `dnsip`—IP address of your Domain Name Server
+   * `gatewayip`—IP address of the Gateway (Router)
+   * `hostname`—Target host name
+   * `ipaddr`—See above
+   * `netmask`—Subnet mask
+   * `rootpath`—Path to the root filesystem on the NFS server
+   * `serverip`—See above
+   * `filesize`—Size in bytes, as a hex string, of the file downloaded using the last `bootp`, `nfs`, or `tftp` command.