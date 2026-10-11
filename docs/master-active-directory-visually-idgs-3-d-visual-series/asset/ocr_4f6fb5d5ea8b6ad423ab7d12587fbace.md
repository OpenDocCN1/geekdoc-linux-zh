# ## CREATING SCOPES

A scope is the total group of IP addresses for a particular subnet. Before creating a scope, you need to know what the starting and ending IP addresses of the scope are. This action determines the number of IP addresses that are in the scope and which IP addresses can be leased to clients. You also need to know the subnet mask for the IP subnet. When the lease is made to the client, the client is provided with both an IP address and the correct subnet mask for the IP subnet. Each subnet must have only one scope.

The scope should contain all IP addresses that can be used in that subnet. This does not mean that all IP addresses within the scope must be available for lease. You can reserve addresses for other uses and create static mappings. The leftover addresses are then used for leasing purposes.

+   1. Select the server, and then choose Action->New Scope.
+   
+   ![Screenshot showing the DHCP management console with the 'New Scope' option selected in the Action menu.](image1)
+   
+   ![Screenshot showing the 'Welcome to the New Scope Wizard' dialog box.](image2)
+   
+   2. Click Next to continue.