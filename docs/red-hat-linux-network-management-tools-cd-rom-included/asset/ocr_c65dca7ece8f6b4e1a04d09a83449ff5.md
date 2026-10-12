Time-stamp: the amount of time between the generation of the Trap and when the device was last initialized, expressed in tens of milliseconds.

Variable-binding: vendor-specific information related to the Trap.

![](bbox=[0.05, 0.26, 0.92, 0.33])

Figure 2.10 Trap message format.

Table 2.5 lists the seven predefined general Trap types. The enterpriseSpecific Trap type is provided as a mechanism to define custom or proprietary traps that do not fit within the other generic types.

# Table 2.5 SNMP predefined traps

| Trap Type | Meaning |
|---|---|
| ColdStart (0) | The device is restarting or reinitializing itself such that the agent or configuration may be changed. Usually, this indicates a crash or other reboot condition |
| WarmStart (1) | The device is restarting or reinitializing itself such that no changes are made to the agent or configuration. Usually, this implies a simple refresh or reboot of the operating system environment |
| LinkDown (2) | Indicates a failure on one of the device's communications (interface) links |
| LinkUp (3) | Indicates a change from a LinkDown state to an operational state |
| Authentication Failure (5) | Indicates the loss of an authentication |
| EgpNeighborChange (6) | Indicates a change in the status of an EGP Neighbor |
| Enterprise-specific | Indicate a custom or proprietary trap from an enterprise |