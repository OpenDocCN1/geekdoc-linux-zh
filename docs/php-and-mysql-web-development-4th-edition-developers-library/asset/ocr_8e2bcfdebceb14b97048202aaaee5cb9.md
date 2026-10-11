+   ▪ --where=where_expr,-w where_expr  
+   Dumps only rows selected by the WHERE condition given by where_expr. You should enclose the condition in quotes to prevent your command interpreter from treating it as multiple command-line arguments.

+   ▪ --xml,-X  
+   Generates output in XML format rather than as a set of SQL statements.

# **F.15.3 Data Format Options for** mysql_dump

If you specify the -tab or -T option to generate a separate data file for each table, several additional options apply. You might need to enclose the option value in appropriate quoting characters. These options are analogous to the data format options for the LOAD DATA statement. See the entry for LOAD DATA in Appendix E.

+   ▪ --fields-enclosed-by=char  
+   Specifies that column values should be enclosed within the given character, usually a quote character. The default is to not enclose column values within anything. This option precludes the use of --fields-optionally-enclosed-by.

+   ▪ --fields-escaped-by=char  
+   Specifies the escape character for escaping special characters. The default is no escape character.

+   ▪ --fields-optionally-enclosed-by=char  
+   Specifies that column values should be enclosed within the given character, usually a quote character. The character is used for non-numeric columns. The default is to not enclose column values within anything. This option precludes the use of --fields-enclosed-by.

+   ▪ --fields-terminated-by=str  
+   Specifies the column value separation character or characters to use for data files. By default, values are separated by tab characters.

+   ▪ --lines-terminated-by=str  
+   Specifies the character or characters to write at the end of output lines. The default is to write newlines.

# **F.15.4 Variables for** mysql_dump

The following mysql_dump variables can be set using the instructions given in Section F.2.1.2,“Setting Program Variables.”