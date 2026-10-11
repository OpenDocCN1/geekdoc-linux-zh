mysql_warning_count was introduced in DBD::mysql 4.004.

# H.4.6  Dynamic Attributes

These attributes are associated with the most recently used handle, represented by $h in the following descriptions. They should be used immediately after invoking whatever handle method sets them, and before invoking another method that resets them.

+   * $rv = $DBI::err;
+       This is the same as calling $h->err().
+   * $str = $DBI::errstr;
+       This is the same as calling $h->errstr().
+   * $rows = $DBI::rows;
+       This is the same as calling $h->rows().

# H.5  DBI Environment Variables

DBI consults several environment variables, listed in Table H.2. All of them except DBI_TRACE are used by the connect() method. DBI_DRIVER is used by the data_sources() method, and DBI_TRACE is used by trace().

Table H.2   DBI Environment Variables

| Name | Meaning |
| :--- | :--- |
| DBI_DRIVER | DBD-level driver name ("mysql" for MySQL) |
| DBI_DSN | Data source name |
| DBI_PASS | Password |
| DBI_TRACE | Trace level and/or trace output file |
| DBI_USER | Username |