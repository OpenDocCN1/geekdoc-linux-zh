# 4.1.3 Guest LAN

Starting with z/VM V4.2, the z/VM Control Program (control program CP) has been enhanced to provide a feature known as Guest LAN. This feature enables you to create multiple Virtual LAN segments within a z/VM environment. As can be seen from Figure 4-2, Guest LANs do not have a physical connection to the external network. Instead, they must use a router (z/VM TCP/IP or Linux). The Linux router or the z/VM TCP/IP stack must have an external interface such as an OSA card, and an interface connected to the LAN.

> Note: Although the structures and the simulated devices related to the Guest LAN under z/VM are virtual, we use the term Guest LAN and not Virtual LAN, because the term Virtual LAN (VLAN) has a different meaning in the networking world.

![](bbox=[0.25, 0.46, 0.88, 0.8])

Figure 4-2 z/VM Guest LAN

# 4.1.4 Virtual Switch

The z/VM Virtual Switch (VSWITCH) introduced with z/VM V4.4 builds on the Guest LAN technology delivered in earlier z/VM releases. VSWITCH connects a Guest LAN to an external interface network using an tOSA card port. Two additional OSA card ports can be specified as backups in the VSWITCH