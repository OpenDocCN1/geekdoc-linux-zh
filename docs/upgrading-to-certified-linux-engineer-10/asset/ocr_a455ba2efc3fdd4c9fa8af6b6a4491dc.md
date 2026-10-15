# Objective 2 Configure DHCP Failover

This objective covers the following topics:

+   - Basics of DHCP Failover
+   - Configure Failover

# Basics of DHCP Failover

The failover protocol allows two DHCP servers (and no more than two) to share a common address pool. Each server will have about half of the available IP addresses in the pool at any given time for allocation.

If one server fails, the other server will continue to renew leases out of the pool, and will allocate new addresses out of the half of available addresses that it had before communication with the other server was lost.

When a server starts that has not previously communicated with its failover peer, it must establish communications and synchronize with the peer before it can serve clients. This can happen either because you have just configured your DHCP servers to perform failover for the first time, or because one of your failover servers has failed and lost its database.

The initial recovery process is designed to ensure that when one failover peer loses its database and then resynchronizes, any leases that the failed server gave out before it failed will be honored. When the failed server starts up, it notices that it has no saved failover state and attempts to contact its peer.