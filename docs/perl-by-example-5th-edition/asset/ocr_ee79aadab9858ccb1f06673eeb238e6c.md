# Examples of Error Messages

The following example shows some common error messages we might receive.

```
EXAMPLE 15.28

1  {Bad Database Name; connect failed}
   DBI connect('sample_db','root',... ) failed: Unknown database
   'sample_db' at first.dbi line 9
2  Bad Password; connect failed}
   DBI connect('sample_db','root',... ) failed: Access denied for user
   'root'@'localhost' (using password: YES) at first.dbi line 9
3  Bad SQL Query; execute failed}
   DBD::mysql::st execute failed: Unknown column 'win' in 'field list' at
   first.dbi line 23.
```

Binding Columns and Fetching Values. Binding columns is the most efficient way to fetch data. Binding allows you to associate a Perl variable with a field (column) value in the database. When values are fetched, the variables are automatically updated with the retrieved value, making fetching data fast. DBI provides the bind_columns method to bind each column to a scalar reference. When the fetch method is called, the values from the database are assigned to scalars of the same name rather than to arrays or hashes as seen in the previous examples.

Every time the fetch method is called, the scalars will be updated with values from the current row.

> (See *bind_col* in the DBI documentation for another way to bind columns.)

```
EXAMPLE 15.29

use DBI;
my $driver="DBI:mysql;
```