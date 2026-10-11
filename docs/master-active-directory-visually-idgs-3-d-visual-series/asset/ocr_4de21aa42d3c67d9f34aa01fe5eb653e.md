# CREATING MULTICAST SCOPES  
CONTINUED

A s with a typical DHCP scope,  
you can set an exclusion  
range for the scope. The  
exclusion range enables you to  
assign static multicast IP addresses  
to certain clients that you choose. In  
some situations, you may choose for  
certain computers or hardware to  
receive a static multicast address.

This is particularly useful for  
network clients that also receive a  
static DHCP IP address. The  
exclusion range, however, must  
leave enough multicast IP addresses  
available in the scope to lease to all  
the clients desired.

As with a standard DHCP lease, you  
can adjust the lease time. The

default lease time for multicast  
addresses is for 30 days. Because  
multicasting is a feature of typical IP  
address leasing for network  
communication, the lease time is  
longer, and this default  
configuration is best under most  
circumstances.

![](bbox=[0.03, 0.5, 0.48, 0.77])

![](bbox=[0.52, 0.5, 0.97, 0.77])

+   **8** Enter a valid Class D  
+   address range for the  
+   multicast scope.
+   
+   ■ You can change the TTL if  
+   needed. The default is 32.

+   **10** Click the arrows to adjust  
+   the TTL value.

+   **8** Click Next to continue.

+   **10** Enter an exclusion range  
+   for the multicast scope, if  
+   desired, then click **Add**.

+   **10** Click Next to continue.