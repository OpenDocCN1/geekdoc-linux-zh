more functionality within Active Directory because it reduces the need to coexist with legacy operating systems. Select **Windows Server 2003** as the forest functional level and then click **Next**.

16. Select **Windows Server 2003** as the domain functional level and then click **Next**.

17. Next, you could select one or more of the following domain controller options for this domain controller:

+   *   **DNS Server**. This option is checked by default and will allow the domain controller to perform DNS name resolution. Leave this box selected.

+   *   **Global Catalog**. This option is selected and grayed out for the first domain controller in a new domain because Active Directory requires that at least one global catalog be installed in each domain.

+   *   **Read-Only Domain Controller (RODC)**. This option is unavailable for the first domain controller in a new domain because the first domain controller cannot be an RODC.

As shown in Figure 2-8, the DNS Server option is selected by default. Click **Next** without making any changes.

# Figure 2-8

Choose additional domain controller options

![](bbox=[0.315, 0.385, 0.65, 0.615])

> See “Working with Read-Only Domain Controllers” later in this lesson for information on the Read-Only Domain Controller.

You may receive a dialog box in step 17 that says “A delegation for this DNS Server will not be created because the authoritative parent zone cannot be found or it does not support dynamic updates. To ensure this DNS Server can be resolved as authoritative for the domain test.com, you can create a delegation to this DNS Server manually in the parent zone. Do you want to continue?” Click Yes to continue. This is a new step in the dcpromo process to ensure that your parent DNS zone (if you have one) contains a delegation for the DNS zone that you are creating. See the article, *Configuring DNS for the Forest Root Domain* on the Microsoft TechNet site for more information.

18. In the window shown in Figure 2-9, you can select the disk locations for the Active Directory database, log files, and the SYSVOL shared folder. Click **Next** to accept the default locations.