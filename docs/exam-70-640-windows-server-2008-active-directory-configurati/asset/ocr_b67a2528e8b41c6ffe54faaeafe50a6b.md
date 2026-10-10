You just configured monitoring of Active Directory performance thresholds using the Reliability and Performance Monitor.

# Diagnosing and Troubleshooting Active Directory

**THE BOTTOM LINE**

After you collect information through your monitoring process, you must understand the tools and techniques used to further investigate a potential problem. For example, the logs available in Event Viewer only record critical events and errors in the Directory Service log. In some cases, by the time the error is recorded, the problem may be serious. To assist you with obtaining more detailed information in the event logs, you can set the event logs to record diagnostic information specific to processes related to Active Directory.

Configuring Active Directory diagnostic event logging requires that you edit the registry. The following key contains the additional areas that can be logged into the Directory Service log:
**HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\NTDS\Diagnostics**

Numerous values are present within the Diagnostics key. Values can be modified to increase or decrease the amount of data that is logged for each event type shown in Figure 11-15.

![](bbox=[0.1, 0.43, 0.88, 0.75])

To increase the level of logging for any event category, double-click a key and modify its value to one of the following:

+   - **0 (None).** Only critical events and error events are logged at this level. This is the default setting for all entries, and it should be modified only if a problem occurs that you want to investigate.
+   - **1 (Minimal).** Very high-level events are recorded in the event log at this setting. Events may include one message for each major task that is performed by the service. Use this setting to start an investigation when you do not know the location of the problem.
+   - **2 (Basic).** This level records slightly more detailed information than the lowest level. Use this setting if Minimal logging is not producing sufficient error messages to allow you to troubleshoot a particular issue.