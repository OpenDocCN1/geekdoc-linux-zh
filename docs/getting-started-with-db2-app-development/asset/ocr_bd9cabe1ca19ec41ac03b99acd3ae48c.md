+   - A class code of 00 means the command was successful.
+   - A class code of 01 implies a warning.
+   - A class code of 02 implies a not found condition.
+   - All other class codes are considered errors.

# B.3 DB2 Administration Notification Log

The DB2 administration notification log provides diagnostic information about errors at the point of failure. On Linux and UNIX platforms, the administration notification log is a text file called <instance name>.nfy (e.g. "db2inst.nfy"). On Windows, all administration notification messages are written to the Windows Event Log.

The DBM configuration parameter **notifylevel** allows administrators to specify the level of information to be recorded:

+   - 0 -- No administration notification messages captured (not recommended)
+   - 1 -- Fatal or unrecoverable errors
+   - 2 -- Immediate action required
+   - 3 -- Important information, no immediate action required (the default)
+   - 4 -- Informational messages

# B.4 db2diag.log

The db2diag.log provides more detailed information than the DB2 Administration notification log. It is normally used only by IBM DB2 technical support or experienced DBAs. Information in the db2diag.log includes:

+   - The DB2 code location reporting an error.
+   - Application identifiers that allow you to match up entries pertaining to an application on the db2diag.logs of servers and clients.
+   - A diagnostic message (beginning with "DIA") explaining the reason for the error.
+   - Any available supporting data, such as SQLCA data structures and pointers to the location of any extra dump or trap files.

On Windows (other than Vista), the db2diag.log is located by default under the directory:

```
C:\Documents and Settings\All Users\Application
Data\IBM\DB2\DB2COPY1\<instance name>
```

On Windows Vista, the db2diag.log is located by default under the directory:

```
C:\ProgramData\IBM\DB2\DB2COPY1\<instance name>
```

On Linux/UNIX, the db2diag.log is located by default under the directory: