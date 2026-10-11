# CONFIGURING ZONE PROPERTIES

The properties sheets for each zone enables you to configure the zone to operate within your environment. As with other server services, you can pause and change the type of service (such as Active Directory integrated) by using the General tab. This feature is particular useful for troubleshooting purposes. An important aspect of the General tab is the dynamic updates section. Windows 2000 supports Dynamic DNS (DDNS) so that database updates can be performed dynamically and not manually by the administrator. The General tab enables you to configure dynamic updates by allowing them, not allowing them, or using only secure updates. In an Active Directory environment, the zones should be allowed to perform dynamic updates. You can use the Start of Authority tab (SOA) to manage the SOA record on your server.

![](bbox=[0.01, 0.53, 0.98, 0.82])

+   1. In the console, select the zone that you want to administer and choose Action->Properties.
+   2. Click these buttons to either pause the zone or to change the type of zone.
+   3. Use this drop-down list to select whether or not to use dynamic updates and the type of update.