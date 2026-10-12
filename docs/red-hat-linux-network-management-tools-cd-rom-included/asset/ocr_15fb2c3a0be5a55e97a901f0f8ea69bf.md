Figure 2.8 shows the packet format that contains the following fields:

+   * *pdu type*: indicates the PDU type is a GetRequest.
+   * *request-id*: unique identifier that permits the SNMP manager to match paired requests and responses. It also aids in detecting duplicate messages that may be received when using an unreliable transport service.

+   * *variable-bindings*: a list of requested MIB objects.

The GetRequest operation is the primary way to obtain information from agents when the objects in question are known beforehand. For example, should the network manager decide to retrieve `sysDescr` and `sysUpTime` objects from an agent, we can think of the request as simply a function to include:

GetRequest (`sysDescr`, `sysUpTime`)

In this case, both of these objects are placed within the variable-binding field when sent. The `sysDescr` object represents a string that contains a general description of the agent, and `sysUpTime` reflects the amount of time that an agent has been running.

![](bbox=[0.05, 0.6, 0.9, 0.71])

When the agent receives the above message and no errors have occurred, it will respond with the values of the MIB objects requested via a GetResponse PDU. The GetRequest operation is atomic. That is, either all the values requested are returned or no values are returned. When the receiving entity responds to the GetRequest, it includes the values in the GetResponse variable-binding field. If, for some reason, at least one of the values cannot be supplied, no values will be provided.