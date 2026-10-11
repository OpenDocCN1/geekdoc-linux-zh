```
ALTER TABLE t ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY;  
ALTER TABLE t ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY FIRST;  
ALTER TABLE t ADD id INT UNSIGNED NOT NULL AUTO_INCREMENT PRIMARY KEY  
    AFTER suffix;
```

+   ADD [COLUMN] (create_definition, . . . )  
+   Adds columns or indexes to the table. Each create_definition is a column or  
+   index definition, in the same format as for CREATE TABLE.

+   ADD [CONSTRAINT [name]] FOREIGN KEY {fk_name}  
+   (index_columns) reference_definition  
+   Adds a foreign key definition to a table. This is supported only for InnoDB tables.  
+   The foreign key is based on the columns named in index_columns, which is a list  
+   of one or more columns in the table separated by commas. Any CONSTRAINT name,  
+   if given, is ignored. fk_name is the foreign key ID. If given, it is ignored unless  
+   InnoDB automatically creates an index for the foreign key; in that case, fk_name  
+   becomes the index name. reference_definition defines how the foreign key re-  
+   lates to the parent table. The syntax is as described in the entry for CREATE TABLE.

```
ALTER TABLE child  
    ADD FOREIGN KEY (par_id) REFERENCES parent (par_id) ON DELETE CASCADE;  
ADD FOREIGN KEY and DROP FOREIGN KEY actions cannot appear in the same  
ALTER TABLE statement.
```

+   ADD [FULLTEXT [INDEX | KEY] [index_name}  
+   (index_columns) {index_option} . . .  
+   Adds a FULLTEXT index to a MyISAM table. The index is based on the columns  
+   named in index_columns, which is a list of one or more non-binary string  
+   columns in the table separated by commas. index_name is specified as for the ADD  
+   INDEX action.

```
ALTER TABLE poetry ADD FULLTEXT (author,title,stanza);
```

+   ADD {INDEX | KEY} [index_name} [index_type]  
+   (index_columns) [index_option] . . .  
+   Adds an index to the table. The index is based on the columns named in  
+   index_columns, which is a list of one or more columns in the table separated by  
+   commas. If the index name index_name is not specified, MySQL chooses a name  
+   automatically based on the name of the first indexed column.