# Chapter 20 Electronic Mail

```
save_to_file:
driver = accept
domains = dialup.example.com
transport = batchsmtp_appendfile
```

The localusers router instance checks that the domain part of the destination address is example.com and that the local part of the address is the login name of a local user. If both conditions are met, the router handles the message to the transport driver instance called my_local_delivery, which is defined in the transports section. The save_to_file instance is designed for dial-up users; it appends the message to a file specified in the batchsmtp_appendfile transport definition.

# The dnslookup router

The dnslookup router is typically used for outgoing messages. It looks up the MX record of the recipient's domain and handles the message to an SMTP transport for delivery. Here is an instance called remoteusers:

```
driver = dnslookup
domains = !+example.com
transport = my_remote_delivery
```

The dnslookup code looks up the MX records for the address. If there are none, it tries the A record. A common extension to this router is to prohibit delivery to IP addresses; a prime example is the RFC1918 private addresses that cannot be routed on the Internet. See the ignore_target_hosts option for more information.

# The manualroute router

The flexible manualroute driver can pretty much route email in whatever way you want. The routing information can be a table of rules matching recipient domain (route_list) or a single rule that applies to all domains (route_data).

Below are two examples of manualroute instances. The first example implements the "smart host" concept, in which all outgoing nonlocal mail is sent to a central ("smart host") host for processing. This instance is called smarthost and applies to all recipients' domains that are not the (! character) in the local_domains list.

```
driver = manualroute
domains = !+local_domains
transport = remote_snmp
route_data = smarthost.example.com
```

The router instance below, firewall, uses SMTP to send messages to hosts inside the firewall (perhaps after scanning for spam and viruses). It looks up the routing data for each recipient domain in the CDB database that contains the names of local hosts. (You must build Exim with the LOOKUP_CDB option to be able to use CDB.)