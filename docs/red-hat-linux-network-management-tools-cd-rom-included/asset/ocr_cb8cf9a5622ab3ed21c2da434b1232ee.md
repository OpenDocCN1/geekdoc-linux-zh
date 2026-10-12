**Object Name:** ifPhysAddress

**OID:** ifEntry.6

**Object Type:** PhysAddress

**Access Mode:** read-only

**Description:** The datalink address of the interface

**Object Name:** ifAdminStatus

**OID:** ifEntry.7

**Object Type:** Integer

**Access Mode:** read-only

**Description:** The administrative status of the interface, which is one of the defined states listed in the `ifOperStatus` object. The owner of the device can control the interface with this object

**Object Name:** ifOperStatus

**OID:** ifEntry.8

**Object Type:** Integer

**Access Mode:** read-only

**Description:** The present operational state of the interface. The defined states include up(1), down(2), and testing(3)

**Object Name:** ifLastChange

**OID:** ifEntry.9

**Object Type:** TimeTicks

**Access Mode:** read-only