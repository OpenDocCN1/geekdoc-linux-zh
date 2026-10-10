Here are some considerations to think about if you want to change the default lease:

+   * Shorter lease times mean unused IP addresses will be placed back into the pool faster. What's more, configuration changes will be recognized faster. However, if a lease expires on a client and that client attempts to connect to the network when the DHCP server is unavailable, the client will not be able to use any network resources until the DHCP server comes back online.
+   * Longer lease times help protect against DHCP server outages. If the DHCP server is down, a client can still connect to the network as long as it has a valid lease on an IP address. However, configuration changes will not be recognized as quickly, and unused IP addresses will be tied up longer.

Once you have filled in all the values here, tab to the <Keep> button and press Enter. This will take you back to the main screen.

# Configuring Fixed-Host Entries

In some situations, you might need to reserve static IP addresses (IP addresses that never change) for some systems, such as for systems that are acting as servers. This arrangement is called a *fixed host*. The second option, DHCP Configurator, allows you to reserve static addresses. Figure 34.5 shows the Fixed-Host Entries configuration dialog.

![](bbox=[0.26, 0.51, 0.74, 0.7])

**FIGURE 34.5**  Configuring information for systems that require static IP addresses.

Table 34.3 shows the options in this dialog and what they do.

**TABLE 34.3 Fixed-Host Configuration Options**

| Option | Description |
| :--- | :--- |
| New entry hostname | This is the hostname of the system that is being configured for static IP. You should provide only the hostname here, not the domain name, because the domain information was provided in the Common options. |
| New entry HW address | Enter the hardware address of the network card on the host that is being configured for static IP here. |
| New entry IP address | This is the static IP address that the host being configured for static IP will use. |