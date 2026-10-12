# ## Testing out distances

Although you may be thrilled to have a wireless LAN working between two computers, you will probably want these computers to be located some distance from each other to make the LAN useful. Getting your wireless LAN to work at the desired distances can be quite a challenge. See the section "Selecting antennas" earlier in this chapter for suggestions on selecting and using antennas to configure the type of wireless LAN you are interested in.

# ## Setting wireless extensions

After the wireless module is loaded, you can change wireless extensions using the `iwconfig` command. The `iwconfig` command is the command that is actually used to set the options added to the `ifcfg` configuration script (for example, for the eth1 interface, the script would be `/etc/sysconfig/network-scripts/eth1`).

Some of the same options that you set when the module was loaded can be reset using the `iwconfig` command. The `iwconfig` command can be useful for testing different settings on an active wireless LAN. The syntax of the `iwconfig` command is as follows:

```
```
# iwconfig interface parameter value
```
```

The *interface* is the name of the wireless interface you want to change, such as eth1 or wvlan0. The *parameter* is the name of the option, and the *value* is replaced by its value. For example, to set your network name (ESSID) to Homelan, you could type the following as root user:

```
```
# iwconfig eth0 essid "Homelan"
```
```

Table 15-2 contains a list of available options for the `iwconfig` command. Refer to the "Configuring the Wireless Interface" section for further details on these options.

## Table 15-2: Options to the iwconfig Command

| Option | Description |
| :--- | :--- |
| essid *name* | Indicates the network name. |
| ap *address* | Indicates that the access point is at a particular MAC address. For low-quality connections, the client driver may return to trying to automatically detect the access point. This setting is only useful in Managed mode. |
| channel *#* | Picks the channel number to operate on. |
| frag *frag_size* | Sets the fragmentation threshold for splitting up packets before they are transmitted. |
| freq 2.4??G | Sets the frequency of the channel to communicate on. |
| key *xxxx-xxxx-xx* | Sets the key used for WEP encryption. |