The capital X switch will disable the channel hopper, if it is not already disabled.

```
-f, --config-file <file>
Use alternate config file
```

If you need to specify an alternate location or an alternate filename for your config file, the -f switch will do that for you.

```
-c, --capture-source <src>
Packet capture source line (type,interface,name)
```

Sometimes you need to specify another capture source. Much like in the config file, it consists of the type (see the README for allowed types), the interface name, and a description with no spaces and all comma separated.

```
-C, --enable-capture-sources Comma separated list of named packet sources to use.
```

If you have multiple sources in your config file, you can fine tune which ones are enabled with the -C switch and listing the descriptions you included in the config file.

```
-p, --port <port>
TCPIP server port for stream connections
```

Due to firewalls or other restrictions, you may need to specify an alternate port to serve up connections from on the drone. If you do so, you'll have to adjust the source= line on your server system to connect to the new port.

```
-a, --allowed-hosts <hosts> Comma separated list of hosts allowed to connect
```

To add a host to allow connections from temporarily, use the -a switch and the IP address.

```
-b, --bind-address <address>
Bind to this address. Default: INADDR_ANY.
```

On multi-homed systems the drone defaults to accepting connections from any configured address. If you want to restrict connections to one address, use the -b switch.

```
-s, --silent
Don't send any output to console.
```

Particularly useful in testing is to suppress output from the drone when it runs.

```
-N, --server-name
Server name
```

For organizational purposes, you can change the server's name. This doesn't show up anywhere major with drones, so no need to worry about it.

```
-v, --version
Kismet version
```

-v outputs the version of the kismet_drone

```
-h, --help
What do you think you're reading?
```

If you find yourself without this book handy, the -h switch will show you the options available.