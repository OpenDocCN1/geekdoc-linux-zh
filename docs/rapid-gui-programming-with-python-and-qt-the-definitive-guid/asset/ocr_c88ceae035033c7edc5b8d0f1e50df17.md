```
query.exec_("""CREATE TABLE calls (
  id INTEGER PRIMARY KEY AUTOINCREMENT UNIQUE NOT NULL,
  caller VARCHAR(40) NOT NULL,
  starttime DATETIME NOT NULL,
  endtime DATETIME NOT NULL,
  topic VARCHAR(80) NOT NULL,
  outcomeid INTEGER NOT NULL,
  FOREIGN KEY (outcomeid) REFERENCES outcomes)""")
```

We have not specified a particular database connection to use, so PyQt will use the default (unnamed) connection that we established earlier. The tables created by the SQL calls are shown schematically in Figure 15.1.

The AUTOINCREMENT syntax tells SQLite to populate the id field automatically with each ID being one more than the previous one, with the first being 1. Similarly, the FOREIGN KEY syntax tells SQLite about a foreign key relationship. SQLite 3 does not enforce foreign key relationships, merely allowing us to express them as a documentation aid. The syntax for achieving automatic IDs and for foreign keys may be different in other databases.

![](bbox=[0.33, 0.5, 0.67, 0.65])

# **Figure 15.1** *The Phone Log database design*

Many databases have their own set of data types. For example, SQLite 3 has what it calls “storage classes”, including INTEGER, REAL, and TEXT. PyQt supports the standard SQL datatypes, including VARCHAR, NUMBER, DATE, and DATETIME, transparently converting to and from the database’s native data types behind the scenes. For text, PyQt uses Unicode, except with databases that don’t support Unicode, in which case PyQt converts to and from the database’s native encoding.

Now that we have created the tables, we can populate them with data.

```
for name in ("Resolved", "Unresolved", "Calling back", "Escalate",
             "Wrong number"):
    query.exec_("INSERT INTO outcomes (name) VALUES ('%s')" % name)
```

We did not need to provide IDs since we have asked the database to generate them for us. Unfortunately, the preceding code is not robust: For example, it will fail if one of the names contains a single quote. One way to deal with this