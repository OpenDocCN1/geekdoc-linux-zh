# The IS-IS Protocol

There is one protocol gated supports that is not being covering in any detail, but you should be aware of in case you require it. It's the Intermediate System-Intermediate-System (IS-IS) protocol. This routing protocol is for internal use in cases where there is a large variety of subnets running on many kinds of networking hardware and software.

IS-IS is a connectionless protocol, meaning that it does not maintain open connections with the machines it exchanges information with—making it more like UDP than TCP; to give you a reference point. If you think you might require the use of this protocol, you can learn more about it starting with RFC 1142 or preferably the ISO DP 10589 parent document.

# Configuring SNMP Interaction

Let's switch gears away from routing protocols and look at the Simple Network Management Protocol (SNMP). Administrators use this tool to aid in managing large computer networks. The gated daemon does not actually run the SNMP protocol, but it does allow your Linux (or other) routers to interface with SNMP if you are using it as part of your network management solution. See RFC 1157 for more about SNMP itself.

The configuration statement for SNMP interactions is actually quite short. It starts, predictably, with:

```
snmp on {
```

Within the parentheses, there are only three options available:

+   - debug;: If you are having troubles with the SNMP daemon on your Linux box, add this line to activate the debugging features.

+   - port value;: If you are running SNMP but have set it to use a port that is not the default port 167, use this statement to tell gated.

+   - traceoptions options. As usual, you use this statement to configure logging. You have access to all of the items available in Table 5.11, as well as those listed in Table 5.23.

# Table 5.23 Options Available for the traceoptions Portion of gated's SNMP Setup

| Option | Purpose |
| --- | --- |
| receive | To log SNMP requests that come from the Linux SNMP daemon, as well as the responses sent to them. |
| register | To log SNMP requests to create new variables. |
| resolve | To log SNMP requests for the contents of a variable. |
| trap | To log SNMP trap messages. |