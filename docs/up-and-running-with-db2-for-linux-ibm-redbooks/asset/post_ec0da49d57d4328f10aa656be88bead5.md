
## Figure 6-4 Start Contacts management

Within the Contacts window, you can add or change contacts or contact groups, or remove unwanted contacts or contact groups. In addition, you can also verify if the e-mail specified for the contact is reachable by pressing a Test button (Figure 6-5).

## Figure 6-5 Contacts management

After pressing the Test button, if the DB2 Message returned shows that the test is successful, then an e-mail will be sent to the specified e-mail account (Figure 6-6).

![](img/d95c931f4f3da4a6bd0ee55148fefad7_243_0.png)

Figure 6-6 The testing e-mail sent by DB2 automatically

> Note: Before using the e-mail notification function, you need to make sure the e-mail system which is residing on the server (specified by SMTP_SERVER in administration configuration) is up and running normally.

After your contact list is added, you can select Configure -> Notifications from the pop-up window, as shown in Figure 6-3, to add or change a contact or contact group. The people in the notification list will be informed if any alert is generated with a severity covered by the current notify level setting. By default, the notification information will be written into DB2 instance's notification log which is located under directory $HOME/sqllib/db2dump, file name is <instance name>.nfy. For details regarding the notification log as well as its setting, refer to 6.2.1, "DB2 administration notification log" on page 242.

## Usage Sample

The following sample shows you how to configure a health indicator in the Health Center, or by DB2 CLP commands, to monitor DMS table space storage consumption. In this example, we expect when table space utilization, which is measured as the percentage of space consumed, exceeds the predefined threshold values for a warning or alarm, DB2 system will send notification to the administration notification log and the specified contacts by e-mail or pager. You can get recommendations from the Health Center or by DB2 CLP commands for such a situation and take actions accordingly. Furthermore, we also show you how to specify follow-up actions for the occurrence of a warning or alarm for this specific health indicator. You can have the DB2 system take the corrective action automatically when the values for a health indicator setting are exceeded.

The example consists of the following steps:

- 1. Prepare DMS tablespace and table.
- 2. Review health indicator for the DMS tablespace
- 3. Populate a desired amount of data into the tablespace
- 4. Check the notification sent by DB2 system
- 5. Set up additional follow-up actions

These steps are given in detail:

- 1. Prepare DMS tablespace and table.

In our example, a DMS tablespace with raw device container is used. For information about how to use raw device in Linux environment for DB2 UDB, refer to Chapter 2, "Installation" on page 23 in this book. The size of the tablespace is 12 MB at its first creation. After the tablespace is created, a table with a unique index is created within (Example 6-2).

### Example 6-2 Prepare tablespace and table for Health Center

```
db2inst2@UDBLNX08:/db2home/db2inst2/test> cat crt_tbspdms_0.db2
create regular tablespace tbpsdms_0
managed by database
using (DEVICE '/dev/raw/raw1' 12M);
db2inst2@UDBLNX08:/db2home/db2inst2/test> db2 -tvf crt_tbspdms_0.db2
db2inst2@UDBLNX08:/db2home/db2inst2/test> cat emp crt.sql
drop table emp;
CREATE TABLE EMP (ENO INTEGER, LASTNAME VARCHAR(30),
    HIREDATE DATE, SALARY INTEGER)
    in tbpsdms_0;
CREATE UNIQUE INDEX u_emp_eno on EMP(ENO);
db2inst2@UDBLNX08:/db2home/db2inst2/test> db2 -tvf emp crt.sql
```

- 2. Review health indicator settings for the DMS tablespace.

To configure the health indicator for DMS tablespaces in the Health Center, you need to start Database Object Health Indicator setting window first (Figure 6-7).

![](img/d95c931f4f3da4a6bd0ee55148fefad7_244_0.png)

Figure 6-7 Start database object health indicator setting

Within the Configure Database Object Health Indicator Setting window as shown in Figure 6-8, the health indicators are listed on the left side of the window. You can select whether or not to monitor them by toggling the check
