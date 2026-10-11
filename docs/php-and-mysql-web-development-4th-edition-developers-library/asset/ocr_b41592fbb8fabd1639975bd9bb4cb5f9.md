`sex` indicates whether a student is a boy or a girl. It’s an ENUM (enumeration) column, which means it can take only one of the values listed in the column specification: `F` for female or `M` for male. ENUM is useful when you have a restricted set of values that a column can hold. We could have used CHAR(1) instead, but ENUM makes it more explicit what the column values can be. If you forget what the possible values are, issue a DESCRIBE statement. For an ENUM column, MySQL displays the list of legal enumeration values:

```
mysql> DESCRIBE student `sex`;
```

| Field | Type | Null | Key | Default | Extra |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `sex` | enum(`F`,`M`) | NO | | | |

Values in an ENUM column need not be just a single character. The `sex` column could have been defined as something like ENUM('Female','Male') instead.

`student_id` is an integer column that will contain unique student ID numbers. Normally, you’d probably get ID numbers for your students from a central source, such as the school office. We’ll just make them up, using an AUTO_INCREMENT column that is defined in much the same way as the `member_id` column that is part of the `member` table created earlier.

If you really were going to get student ID numbers from the office rather than generating them automatically, you would define the `student_id` column without the AUTO_INCREMENT attribute, but leave in the PRIMARY KEY clause, to disallow duplicate or NULL ID values.

Now, what about the ENGINE clause at the end of the CREATE TABLE statement? This clause, if present, names the storage engine that MySQL should use for creating the table. A “storage engine” is a handler that manages a certain kind of table. MySQL has several storage engines, each with its own properties, as discussed in Section 2.6.1, “Storage Engine Characteristics.”

If you omit the ENGINE clause, MySQL picks a default engine, which usually is MyISAM. “ISAM” stands for “indexed sequential access method,” and the MyISAM engine is based on that access method with some MySQL-specific stuff added. Earlier, we provided no ENGINE clause when creating the Historical League tables (`president` and `member`), so they’ll be MyISAM tables (unless you have reconfigured your server to use a different default engine). For the grade-keeping project, we’re explicitly using the InnoDB storage engine instead. InnoDB offers something called “referential integrity” through the use of foreign keys. That means we can use MySQL to enforce certain constraints on the interrelationships *between* tables, something that is important for the grade-keeping project tables:

+   - Score rows are tied to grade events and to students: We don’t want to allow entry of rows into the `score` table unless the student ID and grade event ID are known in the `student` and `grade_event` tables.