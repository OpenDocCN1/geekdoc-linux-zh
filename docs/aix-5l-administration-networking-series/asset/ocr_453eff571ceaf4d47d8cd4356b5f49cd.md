# WHAT'S IN THE SYSTEM ERROR REPORT?

Whenever an operating system module detects an error, the **erodaemon** is notified via the /dev/error special device file and writes the information to the error log. This information is accessed via the **erprt** command. Entering the **erprt** command with no flags produces the following summary error report:

| IDENTIFIER | TIMESTAMP | T C | RESOURCE_NAME | DESCRIPTION |
| :--- | :--- | :--- | :--- | :--- |
| EAA3D429 | 0430145602 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| EAA3D429 | 0430145602 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| EAA3D429 | 0430145602 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| EAA3D429 | 0430145402 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| EAA3D429 | 0430145402 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| EAA3D429 | 0430145402 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| EAA3D429 | 0430145402 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| EAA3D429 | 0430145402 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| EAA3D429 | 0430145402 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| EAA3D429 | 0430145402 | U S | LVDD | PHYSICAL PARTITION MARKED STALE |
| 08A49C99 | 0430145402 | T H | scsi0 | SCSI BUS ERROR |
| 08A49C99 | 0430145402 | T H | scsi0 | SCSI BUS ERROR |
| 08A49C99 | 0430145302 | T H | scsi0 | SCSI BUS ERROR |
| 08A49C99 | 0430145302 | T H | scsi0 | SCSI BUS ERROR |
| 08A49C99 | 0430145302 | T H | scsi0 | SCSI BUS ERROR |
| 08A49C99 | 0430145302 | T H | scsi0 | SCSI BUS ERROR |
| 08A49C99 | 0430145302 | T H | scsi0 | SCSI BUS ERROR |
| 08A49C99 | 0430145302 | T H | scsi0 | SCSI BUS ERROR |
| 2BFA76F6 | 0430144802 | T S | SYSPROC | SYSTEM SHUTDOWN BY USER |
| 9BCEFDEE | 0430145402 | T O | erodaemon | ERROR LOGGING TURNED ON |
| 192AC071 | 0430144602 | T O | erodaemon | ERROR LOGGING TURNED OFF |

Here we see a unique identifier for each entry, the date and time that it occurred, what type (Pending, Performance, Permanent, Temporary, Unknown, or Informational) of event it was, what class (Hardware, Software, Informational, or Undetermined) of event, the resource that logged the event, and a brief description of the event. It is helpful to know that the timestamp of the event is in MMDDDhhmmYY format. From looking at the summary report here, we can see that at 14:53 on 4/30/02 something happened as the system was booting to **bus 0** that appears to have caused a lot of logical volumes to get marked stale. In order to drill down and get more information on what is going on, enter the **erprt** command with the **-a** flag to display details of all entries, or with the **-a** and **-i [identifier]** flags to get the specifics on a particular error ID.