+   * `REAL_AS_FLOAT`
+       The `REAL` data type becomes a synonym for `FLOAT` rather than for `DOUBLE`.

+   * `STRICT_ALL_TABLES`
+       Enables strict checking of input data values for all storage engines to cause MySQL to reject most invalid values. This mode was introduced in MySQL 5.0.2. Use `TRADITIONAL` to be even more strict.

+   * `STRICT_TRANS_TABLES`
+       Enables strict checking of input data values for transactional storage engines to cause MySQL to reject most invalid values. In addition, enable strict checking for non-transactional storage engines when that is possible (such as for single-row `INSERT` statements). This mode was introduced in MySQL 5.0.2. Use `TRADITIONAL` to be even more strict.

The following table lists the composite SQL modes and shows the set of modes for which each one is shorthand.

| Composite Mode | Constituent Modes |
| :--- | :--- |
| ANSI | `ANSI_QUOTES`, `IGNORE_SPACE`, `PIPES_AS_CONCAT`, `REAL_AS_FLOAT` |
| DB2 | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| MAXDB | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_AUTO_CREATE_USER`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| MSSQL | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| MYSQL323 | `HIGH_NOT_PRECEDENCE`, `NO_FIELD_OPTIONS` |
| MYSQL40 | `HIGH_NOT_PRECEDENCE`, `NO_FIELD_OPTIONS` |
| ORACLE | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_AUTO_CREATE_USER`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| POSTGRESQL | `ANSI_QUOTES`, `IGNORE_SPACE`, `NO_FIELD_OPTIONS`, `NO_KEY_OPTIONS`, `NO_TABLE_OPTIONS`, `PIPES_AS_CONCAT` |
| TRADITIONAL | `ERROR_FOR_DIVISION_BY_ZERO`, `NO_AUTO_CREATE_USER`, `NO_ZERO_DATE`, `NO_ZERO_IN_DATE`, `STRICT_ALL_TABLES`, `STRICT_TRANS_TABLES` |