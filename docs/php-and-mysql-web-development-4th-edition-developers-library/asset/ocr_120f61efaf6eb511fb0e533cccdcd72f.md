Related functions are `mysql_field_tell()` to determine the current column posi-
tion, or `mysql_field_seek()` to select a particular column to be returned by the
next call to `mysql_fetch_field()`.

The following example seeks to the first `MYSQL_FIELD`, and then fetches succesive
column information structures:

```
```c
MYSQL_FIELD   *field;
unsigned int    i;

mysql_field_seek(res_set, 0);
for (i = 0; i < mysql_num_fields(res_set); i++)
{
   field = mysql_fetch_field(res_set);
   printf("column %u: name = %s max_length = %lu\n",
          i, field->name, field->max_length);
}
```
```

+   • `MYSQL_FIELD *`

+     `mysql_fetch_fields(MYSQL_RES *res_set)`;

Returns an array of all column information structures for the result set. These may
be accessed as follows:

```
```c
MYSQL_FIELD   *field;
unsigned int    i;

field = mysql_fetch_fields(res_set);
for (i = 0; i < mysql_num_fields(res_set); i++)
{
   printf("column %u: name = %s max_length = %lu\n",
          i, field[i].name, field[i].max_length);
}
```
```

Compare this to the example shown for `mysql_fetch_field()`. Note that al-
though both functions return values of the same type, those values are accessed us-
ing slightly different syntax for each function. `mysql_fetch_field()` returns a
pointer to a single field structure; `mysql_fetch_fields()` returns a pointer to an
array of field structures.

+   • `MYSQL_FIELD *`

+     `mysql_fetch_field_direct(MYSQL_RES *res_set, unsigned int col_num)`;

Given a column index, returns the information structure for that column. The
value of `col_num` can range from 0 to `mysql_num_fields(res_set)`-1. The results
are unpredictable if `col_num` is out of range.