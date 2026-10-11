# ADMINISTERING THE SITES CONTAINER CONTINUED

The major configuration option you have with the site container properties sheets is security. This tab enables you to determine who can access this container within the Active Directory and what tasks they can perform. The standard permissions for the sites container are Full Control, Read, Write, Create All Child Objects, and Delete All Child Objects. By default the following groups have these rights:

+   - Authenticated users: Read
+   - Domain admins: Read, Write, and Create All Child Objects

+   - Enterprise admins: Full Control (which includes all other permissions)
+   - System: Full Control (which includes all other permissions)

![](bbox=[0.05, 0.48, 0.47, 0.8])

![](bbox=[0.5, 0.48, 0.95, 0.8])

+   6. Select the user(s) or group(s) you want to add permission for.
+   7. Click Add.

+   8. Click OK.

+   9. Click the appropriate check boxes to configure the permissions for the new users or groups.
+   10. Clear this check box if you do not want to allow permissions to be inherited to child objects.