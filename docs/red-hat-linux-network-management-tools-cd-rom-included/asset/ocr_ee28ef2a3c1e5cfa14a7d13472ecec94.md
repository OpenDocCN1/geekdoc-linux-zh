returned, which means that the agent doesn't support the object and it is provided only for compatibility purposes.

# Table 7.7 Comparison of MIB-II and Sun MIB objects

| MIB Object | V A | Access within MIB-II | Access within mibisa | Value within mibisa |
| :--- | :---: | :--- | :--- | :--- |
| sysName | ✓ | read-write | read-only | |
| atIfIndex | ✓ | read-write | read-only | |
| ipDefaultTTL | ✓ | read-write | read-only | |
| ipRouteIfIndex | ✓ | read-write | read-write | (fixed) |
| ipRouteMetric1 | ✓ | read-write | read-write | -1 |
| ipRouteMetric2 | ✓ | read-write | read-write | -1 |
| ipRouteMetric3 | ✓ | read-write | read-write | -1 |
| ipRouteMetric4 | ✓ | read-write | read-write | -1 |
| ipRouteMetric5 | ✓ | read-write | read-write | -1 |
| ipRouteType | ✓ | read-write | read-write | (fixed) |
| ipRouteAge | ✓ | read-write | read-write | 0 |
| ipRouteMask | ✓ | read-write | read-write | (fixed) |