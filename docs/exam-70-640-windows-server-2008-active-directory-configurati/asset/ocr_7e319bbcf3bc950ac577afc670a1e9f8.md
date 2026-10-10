![](bbox=[0.1, 0.07, 0.92, 0.41])

+   3. Click **Add**. The **Key Recovery Agent** selection screen is displayed.
+   4. Confirm that the **Key Recovery Agent** certificate for the kra user account is selected, and then click **OK**.
+   5. Click **OK**. You will be prompted to restart Active Directory Certificate Services. Click **Yes** to continue.
+   6. In the left pane, browse to **Roles** → **Active Directory Certificate Services** → **Certificate Templates**.
+   7. Right-click the LUCERNEPUBLISHING-User-Cert template and click **Properties**.
+   8. Click the **Request Handling** tab.
+   9. Place a checkmark next to the **Archive subject's encryption private key** option, and the **Use advanced symmetric algorithm to send the key to the CA** option. Click **OK**.

PAUSE. You can log off of the CA computer or remain logged on for the remaining exercises.

In the previous exercise, you configured key archival and recovery settings for a Windows Server 2008 CA. Next, you will learn about role-based administration for a Windows Server 2008 CA, as well as performing maintenance for a 2008 CA.

# Maintaining a Windows Server 2008 CA

Like its predecessor, Windows Server 2003, Windows Server 2008 has an overall focus on least-privilege and role-based administration. In the Certificate Services role, this means that multiple predefined roles can each perform a specific set of tasks. In this section, we will discuss each of the available CA roles and the specific privileges held by each one. We will also cover the steps needed to back up and restore the Certificate Services database.