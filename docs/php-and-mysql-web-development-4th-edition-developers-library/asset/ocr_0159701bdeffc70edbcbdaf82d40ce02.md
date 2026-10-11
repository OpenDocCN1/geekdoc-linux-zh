technique known as "parameter binding" (see Section 8.2.7, "Placeholders and Prepared Statements").

If you fetch a single value into a variable, be careful how you write the assignment. If you write the beginning of your loop like this, it will work correctly:

```
```perl
while (my $val = $sth->fetchrow->array () ) {
...
```

```

The value is fetched in list context, so the test will fail only when there are no more rows. But if you write the test like this instead, it will fail in mysterious ways:

```
```perl
while (my $val = $sth->fetchrow->array ()) {
...
```

```

The difference here is that the value is fetched in scalar context, so if $val happens to be zero, undef, or the empty string, the test evaluates as false and terminates the loop, even though you have not yet reached the end of the result set.

The second row-fetching method, `fetchrow_arrayref()`, is similar to `fetchrow_array()`, but instead of returning an array containing the column values for the current row, it returns a reference to an array, or `undef` when there are no more rows. Use it like this:

```
```perl
while (my $ary_ref = $sth->fetchrow_arrayref ()) {
{
    my $delim = "";
    for (my $i = 0; $i < @$ary_ref); $i++)
    {
        $ary_ref->[$i] = "" if !defined ($ary_ref->[$i]); # NULL value?
        print $delim, $ary_ref->[$i];
        $delim = ",";
    }
    print "\n";
}
```

```

You access array elements through the array reference, $ary_ref. This is something like dereferencing a pointer, so you use $ary_ref->[$i] rather than $ary[$i]. To convert the reference to an array, use the `@$ary_ref` construct.

fetchrow_arrayref() is unsuitable for fetching variables into a list. For example, the following loop does not work:

```
```perl
while (my ($var1, $var2, $var3, $var4) = @($sth->fetchrow_arrayref ()) )
{
    # do something with variables
}
```

```

As long as `fetchrow_arrayref()` actually fetches a row, the loop functions properly. But when there are no more rows, `fetchrow_arrayref()` returns `undef`, and `@($undef)` isn't legal. (It's like trying to de-reference a `NULL` pointer in a C program.)

The third row-fetching method, `fetchrow_hashref()`, is used like this:

```
```perl
while (my $hash_ref = $sth->fetchrow_hashref ()) {
...
}
```

```