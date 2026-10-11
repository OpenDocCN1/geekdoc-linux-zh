# # MANAGING SCOPES

Several options within the MMC console's Action menu can help you manage scopes.

First, you can reconcile the scopes. If you suspect that there are missing IP addresses within the scope that should be available, you can run the Reconcile command. This action

checks the database for consistency. If discrepancies exist, a dialog box appears listing the discrepancies; if no discrepancies exist, a message box tells you that the scope is consistent.

You can also use the Action menu to deactivate a scope. When you

deactivate a scope, the DHCP server can no longer use that scope to lease IP addresses to client computers. You could use the deactivation for a number of purposes, especially if you have designed a new scope that you want to implement. Remember that a subnet can only contain one DHCP scope.

![](bbox=[0.03, 0.5, 0.52, 0.81])

![](bbox=[0.52, 0.5, 0.97, 0.81])

# RECONCILING A SCOPE

+   1 Select the scope you want to manage in the console, and then choose Action\Reconcile All Scopes to check for inconsistencies.

+   2 Click Verify to continue.

+   1. The Reconcile All Scopes dialog box appears.