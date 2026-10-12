| Options | Descriptions |
|---|---|
| option ntp-servers ip-address [, ip-address... ]; | Lists addresses of network time protocol servers, in order of preference. |
| option netbios-name-servers ip-address [, ip-address... ]; | Lists the addresses of WINS servers, used for NetBIOS name resolution (for Windows file and print sharing). |
| option netbios-dd-server ip-address [, ip-address... ]; | Lists the addresses of NetBIOS datagram distribution (NBDD) servers, in preference order. |
| option netbios-node-type uint8; | Contains a number (a single octet) that indicates how NetBIOS names are determined (used with NetBIOS over TCP/IP). Acceptable values include: 1 (broadcast: no WINS), 2 (peer: WINS only), 4 (mixed: broadcast, then WINS), 8 (hybrid: WINS, then broadcast). |
| option font-servers ip-address [, ip-address... ]; | Indicates the location of one or more X Window font servers that can be used by the client, listed in preference order. |
| option nisplus-domain string; | Indicates the NIS domain name for the NIS+ domain. |
| option nisplus-servers ip-address [, ip-address... ]; | Lists addresses of NIS+ servers available to the client, in order of preference. |
| option smtp-server ip-address [, ip-address... ]; | Lists addresses of SMTP servers available to the client, in order of preference. |
| option pop-server ip-address [, ip-address... ]; | Lists addresses of POP3 servers available to the client, in order of preference. |
| option nntp-server ip-address [, ip-address... ]; | Lists addresses of NNTP servers available to the client, in order of preference. |
| option www-server ip-address [, ip-address... ]; | Lists addresses of WWW servers available to the client, in order of preference. |
| option finger-server ip-address [, ip-address... ]; | Lists addresses of Finger servers available to the client, in order of preference. |
| option irc-server ip-address [, ip-address... ]; | Lists addresses of IRC servers available to the client, in order of preference. |