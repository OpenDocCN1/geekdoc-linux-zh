# EDITING RAS POLICIES CONTINUED

On the Multilink tab, you can allow multilink connections based on the default server settings, disable multilink, or allow multilink and set the maximum number of ports yourself. If you choose to allow multilink, you should also make a decision about BAP (Bandwidth Allocation Protocol). BAP manages the links within a multilink connection by dropping or adding links based on connection needs. For example, if a multilink connection falls below a certain bandwidth usage percentage, one of the links can be dropped because it is not needed, or vice versa. This feature helps conserve bandwidth so that it can be used for other connections. The default setting is a 50 percent reduction for two minutes. At that time, one of the links is dropped. You can adjust this setting so that the policy is more strict or lenient with bandwidth usage.

On the authentication tab, you can choose to enforce a certain protocol that is required for connection. Your choices are EAP, MS-CHAP v2, MS-CHAP, CHAP SPAP, PAP, or unauthenticated access.

![](bbox=[0.05, 0.45, 0.53, 0.82])

![](bbox=[0.54, 0.45, 0.96, 0.82])

+   7. Click the Multilink tab.
+   8. Click the appropriate radio button to either allow default multilink server settings, disable multilink, or allow multilink.

+   9. Adjust the selection boxes to adjust BAP settings so that connection lines are dropped at a certain bandwidth percentage is reached.

+   10. Click the Authentication tab.

+   11. Click the appropriate check boxes to select an authentication method that you want to enforce. You can select more than one check box as needed.

194