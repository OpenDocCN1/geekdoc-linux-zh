**ifcfg-dev** where *dev* is the system’s name for your network interface. For example, the first Ethernet device would be represented by a script called **ifcfg-eth0**. Inside this script there may exist a line that reads **BOOTPROTO=method** where *method* is one of **dhcp**, **bootp**, or **none**. You’ll want to change that to read **BOOTPROTO=dhcp** if it doesn’t already.

# # Advanced Client Configuration

The preceding section should be everything you need to start using that DHCP server on your network. If, however, you do have a client with special needs, you can provide a configuration file for **dhclient**. In the file /etc/dhclient.conf you can specify what information to request from the server, defaults to use if the server is unable to provide certain information, overrides for some information the server sends, and even fall-back addresses to use on networks without a DHCP server. The format is essentially the same as the server configuration file, except with its own settings. The most common settings are summarized in Table 20-2.

| Setting | Description |
| :--- | :--- |
| timeout time | How long should the client keep trying before giving up? The default is 60 seconds. |
| reboot time | This specifies how long after a reboot the client should try to get the same address it had before. After this time passes, if the client hasn't been able to renew its old address, it gives up and tries to acquire a new address normally. The default is 10 seconds. |
| request option, option, ... | The request statement causes the client to seek specific information from the server. The options listed here correspond to the options available to be specified in the server. The defaults are subnet-mask, broadcast-address, time-offset, routers, domain-name, domain-name-servers, host-name, nis-domain, nis-servers, and ntp-servers. |
| require option, option, ... | Options listed here must be included in the server's offer, or the offer is ignored. |
| send {option declaration, ...} | Here the client can supply options to which it already knows the answers, in which case it helps the server differentiate it from other clients. |
| default option declaration | Specify a value for option in case the server doesn't supply one. |

**Table 20-2** Common Settings Used in DHCP Client Configuration