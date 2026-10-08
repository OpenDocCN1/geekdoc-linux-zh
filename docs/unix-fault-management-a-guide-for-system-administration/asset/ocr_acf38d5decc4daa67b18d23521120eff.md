agement of these types of scenar ios much easier. Correlation tools can also be used to help resolve problems. For example, a network printer may be down to some of the users, but not all. The tools can be used to pinpoint the problem.

We have selected a few event correlation tools to discuss in this section. Many other event correlation products are available. Here is a list of some that are not discussed:

+   - NetCool/OMNibus from Micromuse provides event correlation capabilities. The NetCool/Reporter can generate reports based on events interesting to a particular user.
- Tivoli Enterprise Console, part of Tivoli TME, can be configured to do simple event correlation.
- COMMAND/POST, from Boole & Babbage Inc., does event correlation. It works with Tivoli TME, BMC PATROL, and OpenView.
- InCharge, from System Management Arts (SMARTS), does event correlation. It is preconfigured with information about common network problems. InCharge is integrated with Tivoli TME.

# OpenView Event Correlation Services

HP OpenView provides the Event Correlation Services (ECS) tool that integrates with OpenView NNM and IT/O. ECS can be used to reduce and consolidate events. It can also be used to suppress and reduce event storms. This tool can be configured to filter out unnecessary information and help you identify the root cause of a problem. Using ECS, you only need to be notified of critical events. ECS is capable of receiving events as SNMP traps, CMIP notifications, opcm sg messages, and ASCII events. It can be used to manage networks, systems, databases, and applications and is extensible, so new events/sources are easy to add.

The OpenView ECS product has two major components: the ECS Designer and the ECS Engine. The ECS Engine is a runtime correlation engine. It is the real-time component that acts against defined correlation rules. The ECS Designer is a graphical utility used to simplify developing and designing correlation rules. It also provides simulation capabilities to test rules before deploying them.

A *correlation circuit* in ECS is a collection of nodes that are configured to perform correlation and filtering. ECS can correlate events independent of the order in which they were received. You can also configure ECS to suppress repeated events using a time-based filter.

With the ECS integration in IT/O, correlation of events can be done from multiple devices locally by the agent or centrally at the management server. This not only reduces network traffic, but also allows for the root cause to be determined faster and closer to the source, providing more efficient problem resolution.

Correlation templates are easy to distribute to managed nodes. They are distributed the same way as other IT/O templates. Automatic and operator-initiated actions can also be configured and executed locally, even when the management server is down.