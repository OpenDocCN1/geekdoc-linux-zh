| Option | Description |
| :--- | :--- |
| `interface-interval` *number*; | By default, the server scans the list of interfaces on the system every 60 minutes. If `listen-on` is enabled (defined earlier in this table), `named` begins listening for DNS requests on any new interfaces it finds. If an interface has disappeared, `named` will stop listening to requests on that interface. If this option is set to 0, the server will check for available interfaces only when `named` is started up. |
| `statistics-interval` *number*; | Specifies how often the `named` server generates server statistics and deposits them to the log file. Default is every 60 minutes. If set to 0, no statistics are generated. |
| `topology {` *address-list* `};` | When multiple forwarders exist, `named` shows preference to servers assumed to be closer than others. By default, the `named` server shows preference to itself and then to servers on the same subnet. You can specify another order of preference (the order of the *address-list*). You can also embed sublists representing a group of addresses. For example, in this configuration, \`topology { \ 192.168.3.12; \ { 192.168.11.25; 192.168.42/24; } \ 192.168.8.24; \};\` \ first choice is given to 192.168.3.12, equal preference is shown to 192.168.11.25 and all hosts on the 192.168.42.0 network, and last preference is given to 192.168.8.24. |

Table 10-1 BIND Configuration Options (continued)

# The server Statement

The **server** statement tells BIND specific information about other name servers it might be dealing with. The format of the **server** statement is as follows:

```
server ip-address {
    bogus yes/no;
    transfer-format one-answer/many-answers;
};
```

where *ip-address* is the IP address of the server in question.