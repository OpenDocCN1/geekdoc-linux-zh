+   2.  Select the Default Domain Policy and click *Edit*.
+   3.  Right-click the Default Domain Policy node at the top of the left window pane. Click **GPO Status**, and place a checkmark next to **User Configuration Settings Disabled**, **Computer Configuration Settings Disabled**, or **All Settings Disabled**.

**PAUSE. CLOSE** the GPMC.

You have now modified a GPO to optimize its performance at computer startup and shutdown or user logon and logoff.

# SUMMARY SKILL MATRIX

+   **IN THIS LESSON YOU LEARNED:**
+   
+   *   Most security-related settings are found within the Windows Settings node of the Policies node in the Computer Configuration node of a GPO.
+   *   Policy settings that you wish to apply to all computers or users within a domain should be made within the Default Domain Policy GPO. Generally, domain-wide account policies, such as password policies, account lockout, and Kerberos settings, are modified here.
+   *   Windows Server 2008 provides the ability to configure Fine-Grained Password Policies, which allow multiple password and account lockout policies within a single domain.
+   *   Local policy settings govern the actions users can perform on a specific computer and determine if the actions are recorded in an event log. Create audit policies here.
+   *   Auditing can be configured to audit successes, failures, or both. Plan auditing carefully before implementation. Events that are not important to your documentation and information needs can cause unnecessary overhead when audited. Auditing can be a very important security tool when used prudently.
+   *   Because audited events are recorded in the appropriate event log, it is necessary to understand the Event Log Policy setting area. This area allows control over maximum log sizes, log retention, and access rights to each log.
+   *   Restrictions on group memberships can be accomplished using the Group Restriction Policy setting. Implementing this policy removes group members who are not part of the configured group membership list or adds group members according to a preconfigured list.
+   *   Folder Redirection can be configured for folders located on a local computer within the Documents and Settings folder. The Offline Files settings allow redirected folders to be available when a network connection is not present. These two setting areas complement each other.
+   *   Disk quotas can be used to control storage space on a network drive. Implementing disk quotas allows administrators to have tighter control over drive usage, which can affect tape backup and restore functionality.
+   *   Computer configuration group policies are refreshed every 90 minutes by default. Domain controller group policies are refreshed every 2 minutes. These settings can be altered based on the frequency in which policy changes occur.
+   *   Disabling unused portions of a GPO decreases the time it takes to complete policy processing.