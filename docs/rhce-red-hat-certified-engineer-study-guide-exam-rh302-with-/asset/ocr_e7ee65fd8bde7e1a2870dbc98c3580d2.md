# Chapter 24 • Administering Logs

+   May 10 15:10:01 www xntpd[496]: precision = 13 usec
May 10 15:10:02 www xntpd[496]: read drift of -94.732
➤ from /etc/ntp/drift
May 10 15:11:49 dhcpd: DHCPREQUEST for 192.168.1.90
➤ from 00:e0:98:77:40 via eth1
May 10 15:11:49 dhcpd: DHCPPACK on 192.168.1.90 to 00:e0
➤98:77:08:40 via eth1
May 10 15:17:26 www lpd[11305]: www.azuspacific.com
➤ requests printjob lp1
May 10 15:17:27 kernel: port00: PC-style at 03bc
➤[SPP,PS2]
May 10 15:17:27 kernel: port00: Printer, Hewlett-
Packard HP LaserJet Z2100 Series
May 10 15:17:27 kernel: lp0: using port00 (polling).
➤ (serial 2000050901)
May 11 13:44:05 sbmserver lpd[22139]: sbmserver.azuspacific
➤ requests printjob lp1
May 13 15:13:09 sbmserver ftppd[22243]: ACCESS DENIED (not
in any class) TO usr75-dialup119.mix2.Atlanta.cw.net
➤[66.62.189.121]
May 13 13:15:09 sbmserver ftppd[22243]: FTP LOGIN REFUSED
(access denied) FROM usr75-dialup119.mix2.Atlanta.cw
➤net [66.62.189.121], anonymous
➤ May 13 13:15:10 sbmserver ftppd[22243]: FTP session closed
May 23 02:01:56 sbmserver ftppd[21811]: FTP LOGIN FORM
pool1209.dialup.earthlink.net [209.179.189], jczarne
➤ May 11 23:05:29 sbmserver ftppd[21811]: FTP session closed

Each entry has the general form
`time_stamp host application[process_ID]: message`

where

+   * timestamp is the date and time at which the message was received
* host is the name of the host that originated the message
* application is the name of the application that sent the message
* process_ID is the process number of the application that sent the message

Copyright ©2000 SYBEX, Inc., Alameda, CA  www.sytex.com