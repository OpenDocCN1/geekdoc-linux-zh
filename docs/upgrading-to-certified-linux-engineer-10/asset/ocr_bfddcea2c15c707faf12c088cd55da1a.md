When it has established contact, it asks the peer for a complete copy of its lease database. The peer then sends its complete database and sends a message indicating that it is done. The failed server then waits until MCLT (Maximum Client Lead Time) has passed. Once MCLT has passed, both servers make the transition back into normal operation.

This waiting period ensures that any leases the failed server may have given out while out of contact with its partner will have expired.

While the failed server is recovering, its partner remains in the partner-down state, which means that it is serving all clients. The failed server provides no service at all to DHCP clients until it has made the transition into normal operation.

In the case where both servers detect that they have never before communicated with their partner, they both come up in this recovery state and follow the procedure we have just described. In this case, no service will be provided to DHCP clients until MCLT has expired.

# Configure Failover

In a failover configuration you have to decide which server acts as the primary and which acts as the secondary server. Both servers need to have the same configuration for the basic DHCP service they are sharing. They only differ in the failover setup. Therefore, it is recommended to have a common configuration file on both machines which is included in the file /etc/dhcpd.conf.