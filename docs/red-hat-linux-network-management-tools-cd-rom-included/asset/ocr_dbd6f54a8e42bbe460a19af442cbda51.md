**Access Mode:** read-only
**Description:** The mount point of the file system being monitored by the agent

**Object Name:** diskDevice
**OID:** diskEntry.3
**Object Type:** DisplayString [255]
**Access Mode:** read-only
**Description:** The actual device partition (slice) of the disk mounted

**Object Name:** diskMinimum
**OID:** diskEntry.4
**Object Type:** integer
**Access Mode:** read-only
**Description:** The minimum amount of disk space required, in kilobytes, before the agent triggers an event. This value is specified with this object or the `diskMinPercent` object from the agent configuration file

**Object Name:** diskMinPercent
**OID:** diskEntry.5
**Object Type:** integer
**Access Mode:** read-only