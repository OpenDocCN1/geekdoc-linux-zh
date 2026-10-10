Viewing the verbose status of the UFW firewall provides information that helps to explain its configuration:

+   - Status: UFW service is running and will start on system boot (active), or the services stopped and a system boot does not change this (disabled).
+   - Logging: The service's logging feature can be set to off; log all blocked packets (low), which is the default; log all blocked, invalid, no-policy-match, and new connection packets (medium) with rate limiting; log medium-log-level packets and all other packets (high) with rate limiting; and log everything with no rate limits (full).
+   - Default: Shows the default policy for incoming, outgoing, and routed packets, which can be set to either allow the packet, drop (deny) the packet, or reject the packet and send a rejection message back.
+   - New profiles: Shows the default policy for automatically loading new profiles into the firewall, which can be set to ACCEPT, DROP, REJECT, or SKIP, where ACCEPT is considered a security risk.

The various default UFW policies are stored in the /etc/default/ufw configuration file. When first installed, these settings allow all outgoing connections and block all incoming connections. You can make modifications to the firewall as needed using the ufw command and its various arguments. A few common arguments are shown in Table 18.5.

# TABLE 18.5  The ufw command's commonly used arguments

| Argument | Description |
| :--- | :--- |
| allow Identifiers | Sets the rule identified by Identifiers to allow packets |
| deny Identifiers | Sets the rule identified by Identifiers to deny (drop) packets |
| reject Identifiers | Sets the rule identified by Identifiers to reject packets |
| delete RULE | NUM | Deletes the rule identified by RULE or NUM |
| insert NUM RULE | Inserts the rule at index NUM |
| default POLICY DIRECTION | Modifies the default DIRECTION policy, where POLICY is allow, deny, or reject, and direction is incoming, outgoing, or routed |
| logging LEVEL | Sets the logging level, where LEVEL is on, off, low (default), medium, high, or full |

When creating new UFW rules, you can use either simple or full syntax. Simple syntax involves designating the rule using only the port number or its service name. You can also add the protocol to the port number, as shown in Listing 18.15.