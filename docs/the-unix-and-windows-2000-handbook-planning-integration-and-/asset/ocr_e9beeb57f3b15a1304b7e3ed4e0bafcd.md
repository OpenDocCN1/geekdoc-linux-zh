# Figure 6.19
Add host confirmation window.

![](bbox=[0.24, 0.13, 0.62, 0.32])

3. Click the Add Host button to create the records. You will be prompted to confirm the creation, as shown in Figure 6.19. Click OK to continue.

4. You can continue to add hosts in this manner. When you are done, click the Done button.

Your DNS server is now ready for action. If you need to further customize your server, consult the Windows 2000 documentation for advanced configuration options.

# Dynamic DNS

Dynamic DNS (DDNS) is a new Internet Engineering Task Force (IETF) standard for automatic DNS record updates. Basically, DDNS functions in a similar manner to WINS in that the client machine registers with the DNS server and the DNS entry is updated if necessary. DDNS is also fully integrated with the Windows 2000 Active Directory and DHCP service. The DNS server can also be linked with the WINS server to provide continuity across all Windows 2000 name resolution and registration services. With DDNS, the need to manually edit DNS configuration files is reduced significantly. DDNS also allows services such as LDAP to be registered with the DNS server. With this addition, it is now possible for clients to locate a server providing a specific service simply by querying the DNS server. A sample DDNS session is explained here:

+   1. A client, mycomputer, requests an IP address from the DHCP server.
+   2. The DHCP server assigns an available IP address from the address pool to mycomputer.
+   3. The DHCP server registers the PTR record for mycomputer with the DNS server.
+   4. The client mycomputer registers its own A record with the DNS server.

When a lease for an IP address expires, the DHCP server will remove the appropriate PTR and A records from the DNS server.