Table 8.1 Database Configuration Assistant Default Tablespaces
| Tablespace Name | Description |
| CMWILITE | Stores segments for Online Analytical Processing (OLAP) processing |
| DRSYS | Stores segments needed for Oracle's Context feature |
| EXAMPLE | Stores the segments for the sample schemas (e.g., HR, OE) |
| INDEX | Stores your application indexes |
| SYSTEM | Stores data dictionary segments |
| TEMP | Temporary tablespace used for sorting |
| TOOLS | Stores non-application segments for utilities |
| UNDOTBS | Stores rollback segments |
| USERS | Stores segments created by users |

In addition, having several tablespaces, segregated by function, makes database management and backup activities much easier. For example, putting rollback segments in their own tablespace will help ensure that user transactions will always find adequate space to store their before-image data. Additionally, tablespaces that contain only temporary segments do not need to be backed up since they will not store any application data. In general, you should have at least six tablespaces in your database:

+   1. A SYSTEM tablespace for data dictionary segments. This tablespace is required in every database. No application segments should be stored in the SYSTEM tablespace.
+   2. A tablespace that stores only rollback or undo segments. A detailed discussion of techniques for managing rollback and undo segments is included later in this chapter.