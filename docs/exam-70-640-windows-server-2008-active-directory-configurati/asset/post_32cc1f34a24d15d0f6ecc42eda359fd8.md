
## Group Policy Refresh Intervals

Templates\System\Group Policy node in the Group Policy Object Editor window for a GPO. By default, computer policies are updated in the background every 90 minutes, with a random offset of 0 to 30 minutes.

- **Domain Controllers Group Policy Refresh Interval.** The setting for the refresh interval for domain controllers is located in the Computer Configuration\Policies\Administrative Templates\System\Group Policy node in the Group Policy Object Editor. By default, domain controller group policies are updated in the background every 2 minutes.
- **User Configuration Group Policy Refresh Interval.** The setting for the refresh interval for user policy settings is located in the User Configuration\Policies\Administrative Templates\System\Group Policy node in Group Policy Object Editor for a GPO.

The available period that each background refresh process can be set to ranges from 0 to 64,800 minutes (45 days). If you set the *refresh interval* to zero, the system attempts to update the policy every 7 seconds. This can cause a significant amount of traffic and overhead on a production network and should be avoided except in a lab or test environment. However, setting a policy refresh interval to 45 days is also extreme and should not be implemented unless network bandwidth is at a premium. It is also possible to turn off the background refresh of a Group Policy entirely. This setting is available in the Computer Configuration\Policies\Administrative Templates\System\Group Policy node. This setting prevents any policy refreshes, except when a computer is restarted.

### Manually Refreshing Group Policy

When you modify settings that you wish to be immediately invoked without requiring a restart, a new logon session, or waiting for the next refresh period, you can force a manual refresh. This process uses the **gpupdate.exe** tool. This command-line tool was introduced in *Windows Server 2003*, and it is used in *Windows Server 2003* and *Windows Server 2008* to replace the secedit /refreshpolicy command that was used in *Windows 2000*.

An example of the syntax necessary for **gpupdate.exe** to refresh all the user settings affected by the User Configuration node of the Default Domain GPO is as follows:

```
gpupdate /target:user
```

To refresh the Computer Configuration node policy settings, the syntax would be as follows:

```
gpupdate /target:computer
```

Without the /target switch, both the user and computer configuration policy settings are refreshed.

### Optimizing Group Policy Processing

When processing a policy that uses computer or user settings, but not both, the setting area that is not configured should be disabled for faster processing. For example, if you wish to configure a computer policy that applies to all computers within an OU, you should disable the User Configuration node settings so that the policy processing is faster. When one part of the policy is disabled, that section is ignored and the settings are disregarded. This speeds up the completion of the policy processing, because each setting does not need to be read for changes.

## Optimize Group Policy Processing

**GET READY.** To perform this exercise, you must be logged on to the Active Directory domain using Domain Administrator credentials.

1. Open the Group Policy Management Console (GPMC). Click **Forest: <Forest Name>**, click **Domains**, click **<Domain Name>**, and then click **Group Policy Objects**.
2. Select the Default Domain Policy and click *Edit*.
3. Right-click the Default Domain Policy node at the top of the left window pane. Click **GPO Status**, and place a checkmark next to **User Configuration Settings Disabled**, **Computer Configuration Settings Disabled**, or **All Settings Disabled**.

**PAUSE. CLOSE** the GPMC.

You have now modified a GPO to optimize its performance at computer startup and shutdown or user logon and logoff.

## Summary Skill Matrix

- **IN THIS LESSON YOU LEARNED:**
  - Most security-related settings are found within the Windows Settings node of the Policies node in the Computer Configuration node of a GPO.
  - Policy settings that you wish to apply to all computers or users within a domain should be made within the Default Domain Policy GPO. Generally, domain-wide account policies, such as password policies, account lockout, and Kerberos settings, are modified here.
  - Windows Server 2008 provides the ability to configure Fine-Grained Password Policies, which allow multiple password and account lockout policies within a single domain.
  - Local policy settings govern the actions users can perform on a specific computer and determine if the actions are recorded in an event log. Create audit policies here.
  - Auditing can be configured to audit successes, failures, or both. Plan auditing carefully before implementation. Events that are not important to your documentation and information needs can cause unnecessary overhead when audited. Auditing can be a very important security tool when used prudently.
  - Because audited events are recorded in the appropriate event log, it is necessary to understand the Event Log Policy setting area. This area allows control over maximum log sizes, log retention, and access rights to each log.
  - Restrictions on group memberships can be accomplished using the Group Restriction Policy setting. Implementing this policy removes group members who are not part of the configured group membership list or adds group members according to a preconfigured list.
  - Folder Redirection can be configured for folders located on a local computer within the Documents and Settings folder. The Offline Files settings allow redirected folders to be available when a network connection is not present. These two setting areas complement each other.
  - Disk quotas can be used to control storage space on a network drive. Implementing disk quotas allows administrators to have tighter control over drive usage, which can affect tape backup and restore functionality.
  - Computer configuration group policies are refreshed every 90 minutes by default. Domain controller group policies are refreshed every 2 minutes. These settings can be altered based on the frequency in which policy changes occur.
  - Disabling unused portions of a GPO decreases the time it takes to complete policy processing.

## Knowledge Assessment

### Fill in the Blank

Complete the following sentences by writing the correct word or words in the blanks provided.

1. In a case where multiple GPOs are configured for a particular user, Active Directory will determine which one to apply by using the GPO’s ________________.
2. You can automatically add a technical support user to the local Administrators group of each domain workstation by using ________________.
3. The ________________ command allows you to manually refresh Group Policy settings on a particular computer.
4. ________________ refers to a Group Policy setting that is not removed when the GPO setting reverts to “Not Configured.”
5. You would audit ________________ to determine who is authenticating against your Active Directory domain controllers.
6. Each Active Directory domain controller acts as a(n) ________________ to enable the distribution of Kerberos tickets.
7. ________________ allows you to configure a user’s Documents, Desktop, and other folders so that they are stored on a network drive rather than the local computer.
8. Settings in the ________________ section of Group Policy allow you to configure the maximum allowable clock skew between a client and a domain controller.
9. Auditing for ________________ will alert you when a change is made to User Rights assignments, IPSec policies, or trust relationships.
10. You can create a consistent service startup configuration for multiple computers by using the ________________ node in Group Policy.

### Multiple Choice

Circle the correct choice.

1. What type of object would you create to enable multiple password policies within a Windows Server 2008 domain?
   - a. msDS-MinimumPasswordLength
   - b. msDS-MultiplePasswordPolicies
   - c. PasswordSettingObject (PSO)
   - d. msDS-PasswordObject

2. Which configuration item has a default value of 90 minutes for workstations and member servers, with a random offset of 0 to 30 minutes to optimize network performance?
   - a. Refresh time
   - b. Refresh interval
   - c. Clock skew
   - d. Clock interval

3. To determine which users are accessing resources on a particular member server in an Active Directory domain, which event type would you audit?
   - a. Account logon event
   - b. Policy change event
   - c. Account management event
   - d. Logon event

4. Monitoring a system such as Active Directory for the success and/or failure of specific user actions is called
   - a. auditing
   - b. inspecting
   - c. scanning
   - d. sniffing

5. Which audit category includes events such as server startup and shutdown, time changes, and clearing the security log within the Windows Event Viewer?
   - a. Process tracking
   - b. Privileged use
   - c. System Events
   - d. Policy management
