# **Figure 6-1** NNM displays network segments.

![](bbox=[0.11, 0.15, 0.76, 0.51])

be explored. This can also help to limit the scope of the systems managed from a single management station in your organization.

An operator can navigate through the submaps to find a particular LAN segment containing important systems to monitor. In addition to viewing the overall status of a network device, an operator can drill down to see system information, such as configured network interfaces. A system's standby network interfaces — those without a configured IP address — can also be shown. The icons can help you distinguish between configured and standby interfaces, as shown in Figure 6-2. Icons without an "IP" symbol are standby interfaces.

NNM includes a graphical Event Browser, which displays the events received from systems on the network. Events are sent to the management station as SNMP traps. The trap daemon receives these traps and stores them in a database to maintain an event history. The events can be viewed through the Event Browser, and filters can be used to prevent the operator from being flooded with noncritical information. Filters can be based on several attributes, including the sending system, criticality of the event, or the time. NNM can also process Common Management Information Protocol (CMIP) events for multivendor interoperability.

NNM periodically polls network devices to verify that they are working. If no reply is received, a Node Down event is sent as an SNMP trap and logged in NNM Event Browser. This results in a color change of the graphical icon in NNM that represents the device. NNM's reliance