If `$maxlen` is 0, `undef`, or missing, it defaults to the current value of `$DBI::neat_maxlen`, which itself has a default value of 400.  
Don't use `neat()` for statement construction; if you need to perform quoting or escaping of data values to be placed into a statement string, use placeholders or the `quote()` method instead.

+   • `$str = DBI::neat_list( \@array [ , $maxlen [ , $sep] ] );`
+   
+       Calls `neat()` for each element of the list pointed to by the first argument, joins them with the separator string `$sep`, and returns the result as a single string.
+   
+       The `$maxlen` argument is passed to `neat()` and thus applies to individual arguments, not to the combined result of the `neat()` calls.
+   
+       If `$sep` is missing, the default is ``, ''`.

# H.4 DBI Attributes

DBI provides attribute information at several levels. Most attributes are associated with database handles or statement handles, but not with both. Some attributes, such as `PrintError` and `RaiseError`, may be associated with either database handles or statement handles. In general, each handle has its own attributes, but some attributes that hold error information, such as `err` and `errstr`, are dynamic in that they associate with the most recently used handle.

Attributes passed to `connect()` or `connect_cached()` become part of the resulting database handle returned by those methods.

# H.4.1 Database-Handle Attributes

The attributes in this section are associated with database handles.

+   • `$dbh->{AutoCommit};`
+   
+       This attribute can be set to true or false to enable or disable transaction autocommit mode. The default is true. Setting `AutoCommit` to false enables transactions to be performed, each of which is terminated by calling `commit()` for a successful transaction or `rollback()` to abort an unsuccessful transaction. See also the description of the `begin_work()` database-handle method.

+   • `$dbh->{Statement};`
+   
+       Holds the statement string most recently passed to `prepare()` through the given database handle.