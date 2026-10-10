# # Configuring Key Archival and Recovery

> One of the challenges of managing PKI certificates in an enterprise environment is users losing the private keys associated with their certificates. This can happen for any number of reasons: as a user stored a certificate on a laptop that is lost, stolen, or compromised by a virus; a workstation's operating system becomes corrupted and needs to be reinstalled from scratch and the user does not have a backup copy of her private key; and so on.
> 
> This risk can be alleviated by the use of key archival on one or more *CAs*, which will store an escrow copy of each certificate's private key on the CA in case it needs to be restored. This escrow copy of a private key can be restored by one or more *key recovery agents*, user accounts that are configured with a Key Recovery Agent certificate that allows them to perform this sensitive task.

You can configure a Windows Server 2008 CA to allow a single key recovery agent to recover a private key, or in especially high-security environments you can specify that multiple key recovery agents be required to perform this task. Key archival and recovery is not enabled by default on a Windows Server 2008 Certification Authority; it must be configured manually by an administrator. Only those certificates that are issued subsequent to enabling key archival will be protected by this feature; any certificates that were issued by a CA prior to configuring these settings will not be protected and will need to be reissued by the CA.

# ## CONFIGURE KEY ARCHIVAL AND RECOVERY

**GET READY.** This exercise consists of multiple parts. First you will create a user account to function as a key recovery agent. Then you will configure and publish the appropriate certificate template for use with key archival and obtain a certificate based on this template. Finally, you will configure an existing certificate template to allow key archival. This exercise assumes that you have completed all previous exercises described thus far in this lesson.

# **Part A – Create a User Account to Act as a Key Recovery Agent**

+   1. Log on to RWD CO1 as the default administrator of the lucerne publishing.com Active Directory domain.
+   2. Open a command-prompt window and key the following command: `kdsad user cn=kra, cn=users, dc=lucerne publishing, dc=com -samkd kra -desc "Key Recovery Agent" -pwd MSpress#1.` Close the command-prompt window and log off of RWD CO1.

# **Part B – Configure and Publish a Key Recovery Agent Certificate Template**

+   1. Log on to CA as the default administrator of the lucerne publishing.com domain.
+   2. In the left pane of the Server Manager console, browse to *Roles*\*→Active Directory Certificate Services*\*→Certificate Templates.*
+   3. Right-click the Key Recovery Agent template and select **Properties**. On the General tab, place a checkmark next to **Publish certificate in Active Directory**.
+   4. Click the **Security** tab. Click **Add**. The Select Users, Computers, or Groups screen is displayed.
+   5. Key **kra** and click **OK**. Under the Allow column, place a checkmark next to **Enroll** and click **OK**.
+   6. Drill down to *Roles*\*→Active Directory Certificate Services*\*→lucerne publishing- CA*\*→CA*\*→Certificate Templates.* (Notice that this is different from the Certificate Templates console in Step 2, though the display name is similar.) Right-click the Certificate Templates folder and click **New*\*→Certificate Template to Issue**. Select the Key Recovery Agent template and click **OK**.