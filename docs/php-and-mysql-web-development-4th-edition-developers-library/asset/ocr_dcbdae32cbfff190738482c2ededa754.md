# SQL Syntax Reference

T his appendix describes the syntax for SQL statements provided by MySQL. It has three parts:

+   - SQL statements other than those for compound statements.
+   - SQL statements that are used for compound statements, which are written using `BEGIN` and `END` and can be used for writing stored programs that are stored on the server side (functions, procedures, triggers, and events).
+   - The syntax for writing comments in SQL code. Comments are used to write de-scriptive text that is ignored by the server, and to hide MySQL-specific keywords that will be executed by MySQL but ignored by other database servers.

Statement syntax descriptions use the following conventions:

+   - Square brackets `([])` indicate optional information.
+   - Vertical bars `(|)` separate alternative items in a list. If a list is enclosed in square brackets, one alternative may be chosen. If a list is enclosed in curly brackets `({})`, one alternative must be chosen.
+   - Ellipsis notation `(...)` indicates that the term preceding the ellipsis may be repeated.
+   - `n` indicates an integer.
+   - `'str'` indicates a string value. A quoted value such as `'file_name'` or `'pattern'` indicates a more-specific kind of value such as a filename or a pattern.

Unless otherwise indicated, the statements listed in this appendix have been present in MySQL at least as early as MySQL 5.0.0. Statements that were introduced or that changed in meaning since then are noted.

Some statements have become deprecated, are scheduled to be removed, or (in my opinion) have extremely limited utility, so I have not included them here:

BACKUP TABLE
LOAD DATA FROM MASTER
LOAD TABLE tbl_name FROM MASTER
RESTORE TABLE