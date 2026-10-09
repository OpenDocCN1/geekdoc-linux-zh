# **LPI MANAGING PRINT QUEUES**

When a printer is operating normally, it accepts jobs into its print queue and prints those jobs in the order in which they are received. You can give the command **cupreject** followed by the name of a printer to cause a printer to not accept jobs into its print queue; enter the command **cupaccept** to re-enable it. You can also use **system-config-printer** to control the print queue; refer to “Settings” on page 559. Two factors determine how a printer handles a job: if the printer is accepting jobs and if it is enabled. Table 13-1 on page 560 describes what happens with the various combinations of the two factors.

The utilities that change these factors are **cupdisable**, **cupenable**, **cupreject**, and **cupaccept**. Each utility takes the name of a printer as an argument. The following commands first disable and then enable the printer named HPLJ:

```
# cupdisable HPLJ
# cupenable HPLJ
```

The next commands cause HPLJ to reject and then accept jobs:

```
# cupreject HPLJ
# cupaccept HPLJ
```

# **LPI SHARING CUPS PRINTERS**

This section describes how to use textual tools to share local printers. Alternatively, you can use **system-config-printer** (page 558) to share printers: Display the Server Settings window by selecting menubar: Server→Settings and put a tick in the check box labeled **Publish shared printers connected to this system**. Using this technique allows you to choose whether to share each printer.

IPP facilitates remote printing. The Listen directive in the CUPS configuration file, /etc/cups/cupsd.conf, specifies which IP address and port or which domain socket path CUPS binds to and accepts requests on. The Listen directive has the following format:

```
Listen *IP*:*port* \| *path*
```

where *IP* is the IP address that CUPS accepts connections on, *port* is the port number that CUPS listens on for connections on *IP*, and *path* is the pathname of the domain socket CUPS uses to communicate with printers. CUPS typically uses port 631 and by default binds to localhost. Thus it accepts connections from the loopback service of the local system only. CUPS uses /var/run/cups/cups.sock, a local domain socket, to communicate with local printers. It can also use a Port directive to specify the port number it listens to for HTTP requests.

```
$ grep -i listen /etc/cups/cupsd.conf
# Only listen for connections from the local machine.
Listen localhost:631
Listen /var/run/cups/cups.sock
```

To allow other systems to connect to the CUPS server on the local system, you must instruct CUPS to bind to an IP address that the other systems can reach. First remove or comment out the Listen localhost:631 directive; leave the other Listen directive in place: