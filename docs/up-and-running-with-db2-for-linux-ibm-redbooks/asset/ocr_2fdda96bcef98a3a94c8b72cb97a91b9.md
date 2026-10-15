DB21011I In a partitioned database server environment, only the table spaces on the current node are listed.

```
db2inst1@UDBLNX08:~> db2 "select substr(tbspacename,1,20),tbspaceid,substr(dbpgname,1,15) DBPG,bufferpoolid,substr(ngname,1,15) NGName from syscat.tablespaces where tbspaceid>2"
```

|  | TBSPACEID | DBPG | BUFFERPOOLID | NGNAME |
|---|---|---|---|---|
| TBSP32K0000 | 3 | IBM CATGROUP | 2 | IBM CATGROUP |
| TBSP32KTMP0000 | 4 | IBM TEMPGROUP | 2 | IBM TEMPGROUP |

2 record(s) selected.

```
db2inst1@UDBLNX08:~> db2 "select substr(bpname,1,15) BPName,bufferpoolid,substr(dbpgname,1,15) DBPG,npages,pagesize from syscat.bufferpools"
```

| BPName | BUFFERPOOLID | DBPG | NPAGES | PAGESIZE |
|---|---|---|---|---|
| IBMDEFAULTBP | 1 | - | 1000 | 4096 |
| BP32K0000 | 2 | - | 250 | 32768 |

2 record(s) selected.

In the preceding example, the tablespaces TBSP32K0000 with tablespace ID 3 and TBSP32KTMP0000 with tablespace ID 4 were automatically created by the CREATE TOOLS CATALOG command, each with a pagesize of 32K. The first one is a regular tablespace that is used to store the tasks related tables, and the second one is a temporary tablespace. In addition, a bufferpool named BP32K0000 is created with a pagesize of 32K. You need to recycle the database manager to have the new changes take effect. Before you stop the instance, if you use LIST APPLICATIONS to display current applications, you may find that some applications are connected to the Tools Catalog Database with the Application Name "db2dastm":

Example: B-5 Applications connecting to Tools Catalog Database

```
db2inst1@UDBLNX08:/db2home/dasusr1/das/bin> db2 list applications
```

| Auth Id Agents | Application Name | Appl. Handle | Application Id | DB Name | # of |