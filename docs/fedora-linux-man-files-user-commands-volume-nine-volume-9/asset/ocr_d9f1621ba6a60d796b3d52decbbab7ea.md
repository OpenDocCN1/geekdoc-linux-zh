TCP and unix socket options are given below:

**TCP options: port=port [,host=host] [,to=to] [,ipv4] [,ipv6] [,nodelay]**

**host** for a listening socket specifies the local address to be bound. For a connecting socket species the remote host to connect to. **host** is optional for listening sockets. If not specified it defaults to `0.0.0.0`.

**port** for a listening socket specifies the local port to be bound. For a connecting socket specifies the port on the remote host to connect to. **port** can be given as either a port nuer or a service na. **port** is required.

**to** is only relevant to listening sockets. If it is specified, and **port** cannot be bound, `QEMU` will attempt to bind to subsequent ports up to and including **to** until it succeeds. **to** st be specified as a port nuer.

**ipv4** and **ipv6** specify that either IPv4 or IPv6 st be used. If neither is specified the socket may use either protocol.

**nodelay** disables the Nagle algorithm.

**unix options: path=path**

**path** specifies the local path of the unix socket. **path** is required.

**-chardev udp ,id=id [,host=host] ,port=port [,localaddr=localaddr] [,localport=localport] [,ipv4] [,ipv6]** Sends all traffic from the guest to a remote host over UDP.

**host** specifies the remote host to connect to. If not specified it defaults to `localhost`.

**port** specifies the port on the remote host to connect to. **port** is required.

**localaddr** specifies the local address to bind to. If not specified it defaults to `0.0.0.0`.

**localport** specifies the local port to bind to. If not specified any available local port will be used.

**ipv4** and **ipv6** specify that either IPv4 or IPv6 st be used. If neither is specified the device may use either protocol.

**-chardev msmouse ,id=id** Forward `QEMU`'s elated msmouse events to the guest. **msmouse** does not take any options.

**-chardev vc ,id=id [[,width=width] [,height=height]] [[,cols=cols] [,rows=rows]]** Connect to a `QEMU` text console. **vc** may optionally be given a specific size.

**width** and **height** specify the width and height respectively of the console, in pixels.

**cols** and **rows** specify that the console be sized to fit a text console with the given dimensions.

**-chardev ringbuf ,id=id [,size=size]** Create a ring buffer with fixed size **size**. **size** st be a power of two, and defaults to `64K`.

**-chardev file ,id=id ,path=path** Log all traffic received from the guest to a file.

**path** specifies the path of the file to be opened. This file will be created if it does not