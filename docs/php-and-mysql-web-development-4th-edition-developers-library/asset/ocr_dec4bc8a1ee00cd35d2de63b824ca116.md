What if your query contains calculated columns? For example, you might issue a query that returns values that are calculated as the result of an expression:

```
SELECT CONCAT(first_name, ', ', last_name) FROM president
```

A query that is written like that is unsuitable when fetching rows as objects. The name of the selected column is the expression itself, which isn’t a legal property name. However, you can supply a legal name by giving the column an alias. The following query aliases the column as `full_name`:

```
SELECT CONCAT(first_name, ', ', last_name) AS full_name FROM president
```

If you fetch each row from that query as an object, the alias allows the column to be accessed as `$row->full_name`.

The preceding examples use a row-fetching loop of this form that assigns each row to the `$row` variable:

```
while ($row = $sth->fetch({{fetch_mode}}))
...
handle row ...
```

However, there are other ways to fetch rows. One is to fetch an array and assign the result to a list of variables. For example, to assign the `last_name` and `first_name` columns to variables named `$ln` and `$fn` and print the names in first name, last name order, do this:

```
$stmt = 'SELECT last_name, first_name FROM president';
$sth = $dbh->query ($stmt);
while (list ($ln, $fn) = $sth->fetch (PDO::FETCH_NUM))
printf ('%s %s\n', $fn, $ln);
```

The variables can have any legal names you like, but their order in the `list()` must correspond to the order of the columns selected by the query.

It’s also possible to retrieve individual column values directly into PHP variables. To do this, bind columns of the result set to variables using `bindColumn()`, and fetch rows using the `PDO::FETCH_BOUND` fetch mode. That causes `fetch()` to return `true` while rows remain, and to assign column values to the bound variables for each row fetched:

```
$stmt = 'SELECT last_name, first_name FROM president';
$sth = $dbh->query ($stmt);
$sth->bindColumn (1, $ln);
$sth->bindColumn (2, $fn);
while ($sth->fetch (PDO::FETCH_BOUND))
printf ('%s %s\n', $fn, $ln);
```

To fetch all rows at once into an array, use `fetchAll()`:

```
$rows = $sth->fetchAll ();
```

Like `fetch()`, `fetchAll()` uses the default fetch mode, or accepts an explicit fetch-mode argument.

A statement handle can be used as an iterator without invoking `fetch()` explicitly:

```
foreach ($sth as $row)
printf ('%s %s\n', $row['first_name'], $row['last_name']);
```