Database alias = ITSOSJ
Database name = ITSOSJ
Database directory = SQL00001
Database release level = a.00
Comment = ITSO San Jose
Directory entry type = Home
Catalog database partition number = 0
Database partition number = 0

![](bbox=[0.24, 0.28, 0.82, 0.71])

Figure 3-4 Tablespace container definition

In this window (Figure 3-4) we have to decide where DB2 should store the default tablespace userspace1 and what type it should be. SMS (System Managed Storage) means that the tablespace container is a directory in the given path and all data will stored in them as files. DMS (Data Managed Storage) means that the tablespace container is a pre-allocated file which is controlled by DB2.

In the next two windows we have to decide where the catalog tablespace syscatspace and temporary tablespace temspace1 will be located. We recommend that you allocate temspace1 in a different file system. For more details, refer to the description in 2.2.2, "Storage planning" on page 36.