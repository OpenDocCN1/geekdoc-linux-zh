The action plan specified in the Health Center is triggered by warning or alarm condition. If we had set up the action plan from the beginning, the add container task would have been executed once we populated the data. The result is shown in Figure 6-22.

![](bbox=[0.27, 0.22, 0.85, 0.32])

Figure 6-22 Notification for alert and follow-up task execution

This figure is captured from the e-mail system and it shows an alarm has been triggered on the table space. In our example, we have defined notification to contacts for the task, so the follow-up task's execution message was also sent.

It shows that once the alarm for the tablespace is triggered, the follow-up corrective action is executed automatically without user intervention. Meanwhile, DB2 also automatically notifies the related contacts with the detailed information associated to the alert. After corrective actions take effect, the health indicator will return to the normal state and keep monitoring for the system.

# 6.2 Log files for troubleshooting

In DB2 UDB Version 8, the former diagnostic log file, db2diag.log, which contains most information for troubleshooting is separated into two files. The first one is the DB2 Administration Notification Log (also known as DB2 Notify Log) which is intended for database and system administrators use and the content is easy to understand. The second one is DB2 diagnostic log which is intended primarily for DB2 customer support staff or someone who is familiar with viewing diagnostic log file.

The alert log is deprecated and not recommended to use in DB2 UDB Version 8. If you still want to use alert facility in DB2 UDB Version 8, you can enable it by setting DB2 registry variable DB2_ALERT_LOG to true.

# 6.2.1 DB2 administration notification log

The Notify Log contains user-friendly and national-language enabled messages that can help database administrators to obtain more information associated to specific issues, for example, information which is supplemental to an SQLCODE, information from Health Monitor for health indicators, information from task