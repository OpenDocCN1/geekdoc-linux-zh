| TARGET COMPUTER | SAMPLE WMI FILTER STRING |
|---|---|
| All computers that are running Windows XP Professional | Select * from Win32_OperatingSystem where Caption = "Microsoft Windows XP Professional" |
| All computers that have more than 10MB of available drive space on a C: NTFS partition | Select * from Win32_LogicalDisk WHERE Name= "C:" AND DriveType = 3 AND FreeSpace > 10485760 AND FileSystem = "NTFS" |
| All computers that have a modem installed | Select * from Win32_POTSModem Where Name = "MyModem" |

Do not to overuse WMI filters within a production environment. As a tool for deploying GPOs to the appropriate users and computers, they are very powerful. However, it is important to consider the impact that they will have on the performance of startup and logon processes. WMI filter evaluation creates an additional impact on performance due to the time required to evaluate the criteria. Combining WMI filter evaluation and actual policy application increases the time it takes to deliver a working environment to the user. WMI filters can be created using the Group Policy Management console.

# CONFIGURE WMI FILTERING

GET READY. In this exercise you will create a WMI filter, and then apply that filter to a Group Policy Object.

+   1. **OPEN** the Group Policy Management MMC snap-in. Drill down to *<forest_name>*, click *<domain_name>*, and then click **WMI Filters**.
+   2. Right-click the **WMI Filters** node and click **New**. In the Name and Description fields, enter a name and description for the new WMI filter.
+   3. In the Queries section, click **Add**. The WMI Query window will be displayed. Enter the desired query information and click **OK**.
+   4. Click **Save** to create the WMI filter.
+   5. Navigate to the Group Policy Objects node. Select the GPO to be assigned this WMI filter.
+   6. On the **Scope** tab, select the name of the WMI filter you just created from the WMI Filtering dropdown box. Click **Yes** to confirm your changes.

**PAUSE.** **LEAVE** the Group Policy Management console open for the next exercise.

You have just created a new WMI filter and configured a GPO to apply only to users or computers that fit the criteria of the filter. It is important to not overuse WMI filters, because they can have a negative impact on the performance of your client workstations when logging onto Active Directory.

# Determining and Troubleshooting Effective Policy Settings

Resultant Set of Policy (RSoP) is the sum of the policies applied to a user or computer after all filters, security group permissions, and inheritance settings, such as Block Policy Inheritance and Enforce, have finished processing. As the application of group policies becomes more complex within your Active Directory structure, it can become difficult to predict what the final policy settings will be when all processing is complete. In addition, it may be difficult to trace the origin of a particular outcome due to policy inheritance, policy links, and permission settings.