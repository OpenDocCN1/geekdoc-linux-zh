pagesize of 32K and a bufferpool also with pagesize 32K are created within the database, you can use the commands and SQL statements shown in Example B-4 to check that.

# Example: B-4 New tablespaces and bufferpool created automatically

```
db2inst1@UDBLNX08:~> db2 list tablespaces

Tablespaces for Current Database

Tablespace ID          = 0
Name                   = SYSCATSPACE
Type                   = System managed space
Contents               = Any data
State                  = 0x0000
  Detailed explanation:
    Normal

Tablespace ID          = 1
Name                   = TEMPSPACE1
Type                   = System managed space
Contents               = System Temporary data
State                  = 0x0000
  Detailed explanation:
    Normal

Tablespace ID          = 2
Name                   = USERSPACE1
Type                   = System managed space
Contents               = Any data
State                  = 0x0000
  Detailed explanation:
    Normal

Tablespace ID          = 3
Name                   = TBS32K0000
Type                   = System managed space
Contents               = Any data
State                  = 0x0000
  Detailed explanation:
    Normal

Tablespace ID          = 4
Name                   = TBS32KTMP0000
Type                   = System managed space
Contents               = System Temporary data
State                  = 0x0000
  Detailed explanation:
```