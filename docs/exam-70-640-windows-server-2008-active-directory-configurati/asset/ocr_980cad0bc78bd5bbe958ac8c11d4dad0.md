+   5. Click **Cancel** to close the dialog box.

**PAUSE.** You can close the Active Directory Sites and Services snap-in or leave it open for future exercises.

In the previous exercise, you viewed the replication connections that were configured for a domain controller for intrasite replication.

# Implementing and Managing a Site Plan

> You will create and manage Active Directory sites using the Active Directory Sites and Services MMC snap-in. In addition to the first site that is automatically configured when you create an Active Directory forest, you can create and manage additional sites to better control replication traffic on your network. The following sections discuss the steps necessary to create, configure, and manage your site plan.

# RENAME THE DEFAULT-FIRST-SITE-NAME

**GET READY.** Before you begin these steps, log on to the console of a domain controller or an administrative workstation that has the Active Directory Administrative Tools installed.

+   1. Open Active Directory Sites and Services and expand the Sites folder.
+   2. Right-click the **Default-First-Site-Name** site object, and click **Rename**.
+   3. Key a site name that is appropriate for your environment (Redmond-Site, for example) and press **Enter**.

**PAUSE. LEAVE** the MMC console open to use in the next exercise.

It is not uncommon to rename the Default-First-Site-Name to reflect your overall site strategy. The goal here is to name all elements intuitively, making it easy to understand how they correlate. When naming sites and other related objects, it is best to use only letters, numbers, and the hyphen character.

# CREATE A NEW SITE

**GET READY.** Before you begin these steps, log on to the console of a domain controller or an administrative workstation that has the Active Directory Administrative Tools installed.

+   1. In Active Directory Sites and Services, right-click the **Sites** folder, and select **New Site**.
+   2. In the New Object-Site dialog box, key a site name for the new site that is appropriate for your environment.
+   3. Select **DefaultIPSiteLink** from the list of site names, and click **OK** to complete the site creation. If prompted with an additional information message, read the information presented and then click **OK**.

**PAUSE. LEAVE** the MMC console open to use in the next exercise.

After all sites and subnets are created, you associate the appropriate site link with the site. The procedure for this is outlined in the next section.

# Creating a New Subnet

> Each subnet should correspond to a physical network segment. After you have defined the subnets for your network, you will associate them with the appropriate sites.