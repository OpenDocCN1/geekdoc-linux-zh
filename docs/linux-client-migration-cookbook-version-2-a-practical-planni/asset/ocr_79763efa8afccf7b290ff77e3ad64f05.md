![](bbox=[0.268, 0.08, 0.832, 0.396])

# # Satellite server

The technical architecture of the satellite server consists of a server application on top of a database to contain all of the data about systems, groups, entitlements, channels, packages, and errata. This application has a management Web interface. The communication with the clients is performed through the update2 application and several daemons running on the client.

> Note: In Red Hat Enterprise Linux Version 5, update2 will be replaced by yum.

# # RHN Terminology

In this section, we describe terminology used in discussing the RHN/satellite server. These concepts include:

+   - System
- System group
- System set
- System Entitlement
- Channel
- Channel Entitlement
- Errata
- Action
- Activation key

¹ Copyright 2004 Red Hat, Inc. All rights reserved. Reprinted by permission.