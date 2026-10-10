# Using the Group Policy Management Console

The **Group Policy Management Console (GPMC)** is the Microsoft Management Console (MMC) snap-in that is used to create and modify Group Policies and their settings. The **Group Policy Management Editor** can be opened several different ways, depending on what you wish to accomplish. You can create a GPO and then link it to a domain, site or OU, or create and link a GPO in a single step. The GPMC was not pre-installed in Windows Server 2003; it needed to be downloaded manually from the Microsoft Web site. However, it is now included in Windows Server 2008 by default.

+   CERTIFICATION READY?
+   Create and Apply Group Policy objects (GPOs)

# CREATE AND LINK A GPO TO AN OU

**GET READY.** To complete this exercise, you must be logged on using Domain Administrator credentials.

+   1. To create an OU for this exercise, go to a command prompt and key **dsadd ou  ou=Training,\<DomainDN\>.** (For the lucernepublishing.com domain, for example, key **dsadd ou ou=Training,dc=lucernepublishing,dc=com**), as shown in Figure 7-4.

![](bbox=[0.3, 0.39, 0.81, 0.48])

+   2. Click **Start**, click **Administrative Tools**, and then click **Group Policy Management Console.** Click the plus sign (+) next to lucernepublishing.com.

+   3. Right-click the **Training OU** and select **Create a GPO in this domain, and link it here**, as shown in Figure 7-5.

![](bbox=[0.3, 0.58, 0.88, 0.94])

+   4. Key a name for your GPO and click **OK**.