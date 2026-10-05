# OffSec

Session 1: ENCRYPTED BUT *NOT* VALIDATED
For added security, please ensure the client displays the same string:

```
>> Annoy Mona Spiced Outran Numpy Vikas
This is a command session!
```

That means you can enter a dnscat command such as
'ping'! For a full list of clients, try 'help'.

```
command (pgdatabase01) 1> ?
```

Here is a list of commands (use -h on any of them for additional help):

+   * clear
* delay
* download
* echo
* exec
* help
* listen
* ping
* quit
* set
* shell
* shutdown
* suspend
* unset
* upload
* windows

```
command (pgdatabase01) 1>
```

> Listing 613 - Interacting with the dnscat2 client from the server.

This returns a prompt with a "command" prefix. This is the dnscat2 command session, and it supports quite few options. We can learn more about each command by running it with the --help flag.

Since we're trying to listen in this Module, let's investigate the port forwarding options. We can use listen to set up a listening port on our dnscat2 server, and push TCP traffic through our DNS tunnel, where it is decapsulated and pushed to a socket we specify. Our background on console session by command, let's run listen--help.

```
command (pgdatabase01) 1> listen --help
Error: The user requested help
Listens on a local port and connects to the other side like ssh
-, Usage: listen [<host>:<port> <rhost>:<rport>
--help, : Show this message
```

> Listing 614 - Information on the listener.

According to the help output, listen operates much like ssh-L. And we should be familiar with that by now.

Let's try to connect to the SMB port on HRSHARED, this time through our DNS tunnel. We'll set up a local port, listening on 4455 on the loopback interface of FELINEAUTHORITY, and forwarding to 445 on HRSHARES.

PWK - © 2023 OffSec Services Limited. All rights reserved.

633