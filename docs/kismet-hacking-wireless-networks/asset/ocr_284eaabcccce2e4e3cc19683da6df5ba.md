```
# To assign the same custom hop channel to multiple sources, or to split the
# same custom hop channel over two sources (if splitchannels is true), list
# them all on the same sourcechannels line:
# sourcechannels=prism2a,prism2b,prism2c;1,6,11
```

You can also nest multiple sources in an assigned *sourcechannel*. If *channelsplit=true*, Kismet will cycle through the channels, and make sure that no two sources are on the same channel at the same time, maximizing the time spent on high-usage channels, and making sure not to overlap scanned channels. In the config file example, three sources would cycle through each of three channels without overlapping.

```
# Port to serve GUI data
tcpport=2501
```

Here you can specify what TCP port the server will serve clients on. There should be no real reason to change this setting. If you feel the need to change this, make sure to make the appropriate change in the *kismet_ui.conf* file.

```
# People allowed to connect, comma separated IP addresses or network/mask
# blocks. Netmasks can be expressed as dotted quad (/255.255.255.0) or as
# numbers (/24)
allowedhosts=127.0.0.1
```

This is where remote monitoring can be set up. By default, for security reasons, only the host running the server can connect a client (localhost). If you want to use the Kismet client on another system and connect to a remote server, you need to specify the network address of the host that will be connecting to the server. This is accomplished by appending it to the existing line with a comma and no space.
`allowedhosts=127.0.0.1,192.168.0.34,10.0.50.45`

You can also specify valid netblocks; *allowedhosts=127.0.0.1,192.168.0.0/24* or *allowedhosts=127.0.0.1,192.168.0.0/255.255.255.0* will allow the entire 192.168.0.x netblock to connect.

It is best to limit what hosts can connect. If you’re monitoring your corporate network and you let anyone connect, you could end up giving access to your data dumps to an attacker, since Kismet does not do any authentication beyond this.

```
# Address to bind to. Should be an address already configured already on
# this host, reverts to INADDR_ANY if specified incorrectly.
bindaddress=127.0.0.1
```