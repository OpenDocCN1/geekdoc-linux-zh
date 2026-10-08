# Monitoring Notes

Like MIB-II, the System MIF can be used to get generic system information, such as how long the system has been running and system contact information. It can also be useful for checking for any disk-related errors.

# Software MIF

The DMI Software MIF supplies information about the software products and product bundles installed on the system. Fileset and vendor information are also included. The swlist command provides most of the instrumentation.

# MIF Definition

Listing A-18 shows the complete Software MIF specification, as defined by the DMTF.

**Listing A-18 Software MIF specification.**

```
DMTF
[1] ComponentID
    [1] Manufacturer
    [2] Product
    [3] Version
    [4] Serial Number
    [5] Installation
    [6] Verify
[2] Software Location
    [1] Path
    [2] Catalog
    [3] Dfiles
    [4] Layout Version
    [5] Pfiles
[3] Vendors
    [1] Tag*
    [2] Index*
    [3] Title
    [4] Description
[4] Bundles
    [1] Bundle Software Specification*
    [2] Tag
    [3] Architecture
    [4] Location
    [5] Qualifier
    [6] Revision
    [7] Vendor Tag
    [8] Create Time
    [9] Description
```