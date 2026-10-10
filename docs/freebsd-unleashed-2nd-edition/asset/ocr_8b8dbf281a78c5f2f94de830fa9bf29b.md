The client that is running DHCP will be listening on port 67 for this configuration information from the server. When the client receives this information, it will configure itself to use the information that the server has sent.

# ## IP Address Leases

When the DHCP server assigns an IP address to a client, the client does not own the address. Instead, the address is leased. The lease term is configured on the DHCP server. The information about how long the lease is good for is sent to the client along with the configuration information.

The leasing of IP addresses serves two purposes:

+   - If the DHCP server cannot be contacted, the client will check its database to look for a lease that is still valid. Assuming it has a valid lease, the client can continue to function normally, even if the DHCP server is currently down.
+   - It automatically places unused IP addresses that are not in use back in the pool after the lease expires. This helps conserve IP addresses. For example, when a guest from a branch office visits, he can plug his laptop into your network and be assigned an IP address so that he can use your network. When he leaves, that IP address will eventually expire and be placed back into the pool for others to use. This way, IP addresses are not being wasted on systems that do not exist anymore.

# ## Advantages of DHCP over Static IP Addresses

Depending on your situation, DHCP may have several advantages over simply assigning each system its own static IP addresses. These advantages include the following:

+   - **Ease of maintenance.** DHCP automatically keeps track of which IP addresses are in use and which ones are free. This prevents the system administrator from having to keep track of which IP addresses can be assigned to new clients, as well as having to remember to reclaim old IP addresses when clients are permanently removed from the network. All this is handled automatically with DHCP.
+   - **Ease of installing new clients.** When new clients are installed, you (or the user) do not have to worry about setting up the network information. You can simply ask the new client to obtain its information via DHCP, and all the networking information will be configured automatically.
+   - **Ease of use for travelers.** If your users travel to branch offices, DHCP makes their life a lot easier. With DHCP, they can simply plug their laptops into the network at the branch office and have all the network information configured for them automatically. At the next branch office they go to, they can do the same thing. This way, your users do not have to reconfigure their network settings at each office they