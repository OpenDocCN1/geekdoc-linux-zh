# 22.7  Migrating from MC to LAN Cluster Interconnect (and vice versa)

One of the exciting new features of *TruCluster* Server version 5.1A is the LAN Cluster Interconnect. This functionality opens up far more systems to clustering and the benefits of Single System Image management (which means, for starters, that you only have to install the OS once, applications once, etc.). We’ll show the steps required to migrate from a MEMORY CHANNEL Cluster Interconnect (CI) to a LAN CI. But first, let’s review a few requirements.

The Cluster Interconnect LAN:

+   - Must be private to the cluster members alone.
+   - Can be direct or configured with hubs or switches but not both.
+   - Must disable Spanning Tree Protocol on switch ports that connect to cluster members.
+   - Must configure the switches in a “fully redundant LAN cluster interconnect” so that there is no packet forwarding between them.
+   - Must be 100Mbps or 1000Mbps full duplex throughout the configuration (including switches/hubs). Using the half-duplex option (hubs) is not recommended because of the limited performance of hub technology.
+   - Must be configured such that there is at least one point-to-point path between each member.
+   - Must not be configured with Link Aggregation (LAG).
+   - Must not be configured with more than two switches between any two members.

# 22.7.1  Moving from MEMORY CHANNEL to LAN Cluster Interconnect

Say that you built your cluster at a pre-V5.1A version, upgraded to V5.1A, and now want to try out the LAN CI that you’ve heard so much about. The first thing you should do is take out the *TruCluster* Server Cluster LAN Interconnect manual provided by HP and look in Chapter 4 for the directions. These steps are covered thoroughly in the manual but we’ll go over them briefly here.

To perform this switch from MC to LAN Interconnect, we obviously have to schedule some down time because we’re making a radical change to the medium that the cluster uses to do a whole suite of communicating and in order to install and/or remove hardware.:

+   1. Shut down and power off each member.
+   2. Install the network adapters for the private CI LAN if they aren’t already installed and set the NIC’s mode at the console prompt. For example:

```
>>> set ewa1_mode FastFD
```