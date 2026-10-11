```
mysql_field_seek (res_set, 0);
for (i = 0; i < mysql_num_fields (res_set); i++)
{
 field = mysql_fetch_field (res_set);
 col_len = strlen (field->name);
 if (col_len < field->max_length)
 col_len = field->max_length;
 if (col_len < 4 && !IS_NOT_NULL (field->flags))
 col_len = 4; /* 4 = length of the word 'NULL' */
 field->max_length = col_len; /* reset column info */
}

print_dashes (res_set);
fputc ('|', stdout);
mysql_field_seek (res_set, 0);
for (i = 0; i < mysql_num_fields (res_set); i++)
{
 field = mysql_fetch_field (res_set);
 printf (' %-*s |', (int) field->max_length, field->name);
}
fputc ('\n', stdout);
print_dashes (res_set);

while ((row = mysql_fetch_row (res_set)) != NULL)
{
 mysql_field_seek (res_set, 0);
fputc ('|', stdout);
for (i = 0; i < mysql_num_fields (res_set); i++)
{
 field = mysql_fetch_field (res_set);
 if (row[i] == NULL) /* print the word 'NULL' */
 printf (' %-*s |', (int) field->max_length, "NULL");
 else if (IS_NUM (field->type)) /* print value right-justified */
 printf (' %*s |', (int) field->max_length, row[i]);
 else /* print value left-justified */
 printf (' %-*s |', (int) field->max_length, row[i]);
}
fputc ('\n', stdout);
}
print_dashes (res_set);
printf ('Number of rows returned: %\n',
 (unsigned long) mysql_num_rows (res_set));
```