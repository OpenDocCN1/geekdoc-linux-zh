
box underneath the Evaluate bar, setting the threshold values of warning or alarm, respectively. You can review the commands generated based on your choices by clicking Show Command.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_245_0.png)

Figure 6-8 Configuring database object health indicators

Furthermore, you can set actions when the threshold values reach the warning or alarm level. To set up the action, choose a specific health indicator and click on this health indicator's action property button "...", as shown in Figure 6-9 highlighted in red ellipse. Another window appears, and this window can be used to enable the action property for the health indicator, and run a script or a task which is predefined in the task center.

Figure 6-9 Setting up Action for specific health indicator

The configuration dialog launches in the context of the database selected in the Health Center. To view the tablespace health indicators, we need to choose the database object first. By clicking the "..." button beside Object as shown in the Figure 6-10 (where the button is highlighted in red), the database object list window will pop up. In the pop-up windows, keep expanding the object tree until the desired object is shown, and then select the object and click OK. Here we chose the DMS tablespace which is created beforehand in Step 1 of this example.

![](img/d95c931f4f3da4a6bd0ee55148fefad7_247_0.png)

Figure 6-10 Choosing database object for health indicator setting

Once the object is chosen, you can modify the health indicators settings for database objects. Figure 6-11 shows the default setting from the tablespace level global settings. In our example, a threshold value of 80 is set for a warning. Likewise, another threshold value, 90, is set for alarm, and no action is defined. Both default values are expressed in percentage. To change the threshold value, click the number and a new button will appear for you to specify the new value.

Figure 6-11 Database object health indicator setting

You can click Show Command to get the command based on the above choices, as shown in Figure 6-12. You can run the command in DB2 CLP to change configurations for the health indicator, or click OK to submit your changes.

Figure 6-12 Set health indicator value command

You can use the DB2 CLP command GET ALERT CFG to verify the setting, as shown in Example 6-3.

## Example 6-3 Using GET ALERT CFG to view health indicator status

```
db2inst2@UDBLNX08:/db2home/db2inst2> db2 "get alert cfg for tablespaces "
```

Alert Configuration

Indicator Name = ts.ts_op_status
Type = State-based
Sensitivity = 0
Formula = ts.ts_status;
Actions = Disabled
Threshold or State checking = Enabled

Indicator Name = ts.ts_util
Type = Threshold-based

```
Warning          = 80
Alarm            = 90
Sensitivity       = 0
Formula = ((ts.ts_used_pages/ts.ts_usable_pages)*100);
Actions          = Disabled
Threshold or State checking = Enabled
```

## 3. Populate a desired amount of data into the tablespace.

We populate a certain amount of data into the tablespace to trigger the threshold. DB2 common table expression is used in our example to generate specified number of rows (Example 6-4). In our example 200,000 rows are inserted into the table and consume more than 11 MB space for table data and index pages. The total space for the table space is around 12 MB so the threshold values will be exceeded as expected.

## Example 6-4 Populating data to trigger threshold for table space utilization

```
db2inst2@UDBLNX08:/db2home/db2inst2/test> cat empins.sql
INSERT INTO EMP
WITH DT(ENO) AS (VALUES(1) UNION ALL SELECT ENO+1 FROM DT WHERE ENO < 200000 )
SELECT ENO, TRANSLATE(CHAR(INTEGER(RAND()*1000000)),
        CASE MOD(ENO,4) WHEN 0 THEN 'aeiou' || 'bcdfg'
                     WHEN 1 THEN 'aeiou' || 'hjkIm'
                     WHEN 2 THEN 'aeiou' || 'npqrs'
                     ELSE 'aeiou' || 'twxyz' END,
                     '1234567890') AS LASTNAME,
        CURRENT DATE - (RAND()*10957) DAYS AS HIREDATE,
        INTEGER(10000+RAND()*200000) AS SALARY
FROM DT;

db2inst2@UDBLNX08:/db2home/db2inst2/test> db2 -tvf empins.sql
DB20000I  The SQL command completed successfully.
```

## 4. Check the notification sent by DB2 system.

Once DB2 Health Monitor detected that the threshold for warning or alarm has been exceeded, it will send warning or alarm messages to the DB2 administration notification log as well as specified contacts if you have configured notifications. In our example, the notification will be sent to notification log and to a contact point via e-mail.

We can use DB2 Journal to check the administration notification log. To start the DB2 Journal, select Tools → Journal in any DB2 Tools window, where the Tools menu is available, or from Health Center, right-click on the instance name and select Show Notification Log. Then select the Notification Log tab, choose Instance to view the notification log. The instance in our example is db2inst2. The notification log for the instance will be shown in the bottom pane of the window. You also can use the Notification Log Filter to set up a
