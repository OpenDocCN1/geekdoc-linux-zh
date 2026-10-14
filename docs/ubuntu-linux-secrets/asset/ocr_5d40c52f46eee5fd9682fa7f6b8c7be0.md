# Table 20-4: (continued)

| Option | Description |
|---|---|
| type=value | Same as querytype |
| [no]recurse | Tell nameserver to query other servers to obtain an answer (default = recurse) |
| retry=number | Set number of retries to number (default = 4) |
| root=host | Change name of root server to host (default = ns.internic.net) |
| timeout=number | Change initial timeout interval to wait for a reply to number (default = 5 seconds) |
| [no]vc | Always use a virtual circuit (default = novc) |
| [no]ignoreetc | Ignore packet truncation errors (default = noignoreetc) |

Let's take a look at a sample nslookup session used to get information for host www.ubuntu.com:

```
$ nslookup
> www.ubuntu.com
Server: 10.0.1.1
Address: 10.0.1.1#53

Non-authoritative answer:
Name: www.ubuntu.com
Address: 91.189.94.249
>
```

When you enter nslookup on the command line, it produces its own command-line prompt, the greater-than sign (>). At this point, you can enter a command or the hostname you want to find information for.

The following example shows retrieving the basic IP address information on a typical hostname. You can also set the output for a specific type of DNS record to retrieve that information:

```
> set type=MX
> ubuntu.com
Server: 10.0.1.1
Address: 10.0.1.1#53

Non-authoritative answer:
ubuntu.com mail exchanger = 10 mx.canonical.com

Authoritative answers can be found from:
>exit
$
```

In this example, I set the record type to MX to return the mail servers for the domain.