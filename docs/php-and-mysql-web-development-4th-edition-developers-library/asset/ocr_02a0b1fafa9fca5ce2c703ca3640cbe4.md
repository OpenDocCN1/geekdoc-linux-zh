+   - Grant an account read-only privileges for the tables in the `managerie` database. The `lookonly` user can connect from any host in the `xyz.com` domain:
+     ```sql
+     GRANT SELECT ON managerie.* TO 'lookonly'@'%.xyz.com';
+     ```
+   - Grant an account full privileges, but only for the `member` table in the `samppdb` database. The `member_mgr` user can connect from a single host:
+     ```sql
+     GRANT ALL ON samppdb.member TO 'member_mgr'@'boá.make.net';
+     ```
+   - Grant an account superuser privileges, including the ability to grant privileges to other users. The user must connect from the local host:
+     ```sql
+     GRANT ALL ON *.* TO 'superduper'@'localhost' WITH GRANT OPTION;
+     ```
+   - Grant an anonymous user full access to the `managerie` database:
+     ```sql
+     GRANT ALL ON managerie.* TO ''@'localhost';
+     ```
+   - Grant an account full access to the `privatedb` database, but require that connections be made via SSL with a valid X509 certificate:
+     ```sql
+     GRANT ALL ON privatedb.* TO 'Paranoid'@'%.mydomain.com' REQUIRE X509;
+     ```
+   - Grant an account limited access such that it can issue only 100 statements per hour, of which at most 10 may be updates:
+     ```sql
+     GRANT ALL ON test.* TO 'caleb'@'localhost'
+     WITH MAX_QUERIES_PER_HOUR 100 MAX_UPDATES_PER_HOUR 10;
+     ```

# HANDLER

```
HANDLER *tbl_name* OPEN [AS] *alias_name*

HANDLER *tbl_name* READ

[FIRST | NEXT]

[where_clause] [limit_clause]

HANDLER *tbl_name* READ *index_name*

[FIRST | NEXT | PREV | LAST | < | <= | = | >= | >] (*expr_list*)

[where_clause] [limit_clause]

HANDLER *tbl_name* CLOSE
```

HANDLER provides a low-level interface to the MyISAM and InnoDB storage engines that bypasses the optimizer and accesses table contents directly. To access a table through the HANDLER interface, first use HANDLER ... OPEN to open it. The table remains available for use until you issue a HANDLER ... CLOSE statement to close it explicitly or until or the connection terminates. While the table is open, use HANDLER ... READ to access the table's contents.