```
/* determine column display widths -- requires result set to be */
/* generated with mysql_store_result() not mysql_use_result() */
mysql_field_seek (res_set, 0);
for (i = 0; i < mysql_num_fields (res_set); i++)
{
field = mysql_fetch_field (res_set);
col_len = strlen (field->name);
if (col_len < field->max_length)
col_len = field->max_length;
if (col_len < 4 && !IS_NOT_NULL (field->flags))
col_len = 4; /* 4 = length of the word "NULL" */
field->max_length = col_len; /* reset column info */
}
```

This code calculates column widths by iterating through the MYSQL_FIELD structures for the columns in the result set. We position to the first structure by calling mysql_field_seek(). Subsequent calls to mysql_fetch_field() return pointers to the structures for successive columns. The width of a column for display purposes is the maximum of three values, each of which depends on metadata in the column information structure:

+   - The length of field->name, the column title.
+   - field->max_length, the length of the longest data value in the column.
+   - The length of the string "NULL" if the column can contain NULL values.
+   field->flags indicates whether the column can contain NULL.

Notice that after the display width for a column is known, we assign that value to max_length, which is a member of a structure that we obtain from the client library. Is that allowable, or should the contents of the MYSQL_FIELD structure be considered read-only? Normally, I would say "read-only," but some of the client programs in the MySQL distribution change the max_length value in a similar way, so I assume that it's okay. (If you prefer an alternative approach that doesn't modify max_length, allocate an array of unsigned long values and store the calculated widths in that array.)

The display width calculations involve one caveat. Recall that max_length has no meaning when you create a result set using mysql_use_result(). Because we need max_length to determine the display width of the column values, proper operation of the algorithm requires that the result set be generated using mysql_store_result(). In programs that use mysql_use_result() rather than mysql_store_result(), one possible workaround is to use the length member of the MYSQL_FIELD structure, which tells you the maximum length that column values can be.

When we know the column widths, we're ready to print. Titles are easy to handle. For a given column, we simply use the column information structure pointed to by field and print the name member, using the width calculated earlier:

```
printf (" %-*s |", (int) field->max_length, field->name);
```