**Description:** The list of load average names that the agent is monitoring. This can be one of the three load average windows that the agent supports: one, five, and 15 minutes. These are represented by the strings Load-1, Load-5, and Load-15, respectively

**Object Name:** laLoad

**OID:** laEntry.3

**Object Type:** Display String [255]

**Access Mode:** read-only

**Description:** The actual system load averages for one, five, and 15 minutes, as recorded by the agent

**Object Name:** laConfig

**OID:** laEntry.4

**Object Type:** Display String [255]

**Access Mode:** read-only

**Description:** Contains the watch threshold for the load average to signal an error. This object obtains its value for the agent configuration file using the `load` command

**Object Name:** laErrorFlag

**OID:** laEntry.100

**Object Type:** Integer

**Access Mode:** read-only