```
my $value = $sth->($stmt_attr)->{$i};
}

```

The NAME_hash, NAME_lc_hash, and NAME_uc_hash attributes return a reference to a hash. You can loop through the hash elements like this:

```
foreach my $key (keys (${$sth->{$stmt_attr}}))
{
    my $value = $sth->($stmt_attr)->{$key};
}

```

+   - `Sary_ref = $sth->{NAME};`
+   - A reference to an array of strings indicating the name of each column. The letter-case of the names is as specified in the `SELECT` statement.
+   - `Sary_ref = $sth->{NAME_hash};`
+   - A reference to a hash of strings indicating the name of each column. The lettercase of the names is as specified in the `SELECT` statement. The value of each hash element indicates the position of the corresponding column within result set rows (beginning with 0).
+   - `Sary_ref = $sth->{NAME_lc};`
+   - Like `NAME`, but the names are returned as lowercase strings.
+   - `Sary_ref = $sth->{NAME_lc_hash};`
+   - Like `NAME_hash`, but the names are returned as lowercase strings.
+   - `Sary_ref = $sth->{NAME_uc};`
+   - Like `NAME`, but the names are returned as uppercase strings.
+   - `Sary_ref = $sth->{NAME_uc_hash};`
+   - Like `NAME_hash`, but the names are returned as uppercase strings.
+   - `Sary_ref = $sth->{NULLABLE};`
+   - A reference to an array of values indicating whether each column can be `NULL`. Values for each element can be 0 or an empty string (no), 1 (yes), or 2 (unknown).
+   - `Srv = $sth->{NUM_OF_FIELDS};`
+   - The number of columns in a result set, or zero for a non-`SELECT` statement.
+   - `Srv = $sth->{NUM_OF_PARAMS};`
+   - The number of placeholders in a prepared statement.
+   - `Sary_ref = $sth->{PRECISION};`
+   - A reference to an array of values indicating the precision of each column. DBI uses "precision" in the ODBC sense, which for MySQL means the maximum width of the column. For numeric columns, this is the display width. For string columns, it’s the maximum length of the column, in octets (bytes), not characters.