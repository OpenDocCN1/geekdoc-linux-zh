allowed only at the primary prompt and disallowed at the secondary prompts. (That is, they are disallowed on second and subsequent lines of a multiple-line statement.)

+   ■ `--no-auto-rehash`, `-A`
+   This option is deprecated in favor of `--skip-auto-rehash`. See the description for `--auto-rehash`.

+   ■ `--no-beep`, `-b` *(boolean)*
+   Suppresses production of beeps when errors occur.

+   ■ `--no-named-commands`, `-g`
+   This option is deprecated. See the description for `--named-commands`.

+   ■ `--no-pager`
+   This option is deprecated in favor of `--skip-pager`. See the description for `--pager`.

+   ■ `--no-tee`
+   This option is deprecated in favor of `--skip-tee`. See the description for `--tee`.

+   ■ `--one-database`, `-O`
+   This option is used when updating databases from the contents of a binary log file. It tells *mysql* to update only the default database (the database named on the command line). Updates to other databases are ignored. If no database is named on the command line, no updates are performed.

+   ■ `--pager`[*=program*]
+   The name of a paging program to use for displaying long query results one page at a time (for example, /bin/more or /bin/less). If *program* is missing, the paging program is determined from the value of the PAGER environment variable. Output paging is unavailable in batch mode, and does not work under Windows. Paging can be disabled with `--skip-pager`.

+   ■ `--prompt`*=str*
+   Changes the primary prompt from *mysql>* to the string defined by *str*. The string can contain special sequences, as described in Section F.5.5, "mysql Prompt Definition Sequences."

+   ■ `--quick`, `-q`
+   Normally *mysql* retrieves the entire result of a query from the server before displaying it. This option causes each row to be displayed as it is retrieved, which uses much less memory and may allow some large statements to be performed successfully that would fail otherwise. However, this option should not be specified for interactive use; if the user pauses the output or suspends *mysql*, the server continues to wait, which can interfere with other clients.