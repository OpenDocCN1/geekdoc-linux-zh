# **Figure 3-2** IT/O template distribution.

![](bbox=[0.09, 0.14, 0.95, 0.44])

IT/O also enables you to create your own monitors and templates. For instance, you can create a template to monitor arbitrary MIB variables, such as network interface status. The IT/O agent then periodically queries the MIB object to determine whether a message should be generated. Or, you can create your own monitor program or script that is invoked periodically by the IT/O agent. These monitors or scripts can have notifications sent by the IT/O agent, or they can send IT/O notifications through the opcom API. The monitor can then send asynchronous events, which is often more efficient than a polling mechanism. The IT/O user interface can also be used to set up monitoring of a specified log file, such as the system log file. Thus, an easy way to integrate a new monitor is to have interesting events first written to a log file.

# **Notification Methods**

IT/O is capable of receiving events via SNMP traps. IT/O also forwards events from the IT/O agent to the management station, using opcomsg. Local agents can buffer events if the management station is temporarily unavailable.

The opcom API can be used to forward the current value of a monitored object to the IT/O agent. The agent then checks the value against the configured threshold. If the threshold is met, the event is forwarded to the IT/O management station. Local actions, which may include logging or suppressing the message, are done before the message is forwarded. Additionally, message templates can be configured with automatic actions, such as generating an e-mail message or pager notification.

IT/O also provides a capability called "follow the sun," which enables events to be forwarded to the appropriate IT/O management station in a global environment based on the time of day. For example, if you have data centers with management stations in Japan, Europe, and