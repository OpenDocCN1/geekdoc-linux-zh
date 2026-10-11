# EXAMPLE 15.41 (CONTINUED)

```
```
9    state $html = do { local $/; <DATA> };
10   my $dbh = DBI->connect("DBI:mysql:host=localhost;
               database=sample_db;user=root;password=quigley!"
11               or die "Connection to sample_db failed: $DBI::errstr";

12   my $sth = $dbh->prepare("SELECT * FROM coaches");
13   $sth->execute();
14   my $rows = $sth->fetchall_arrayref();

15   return (engine 'template')->render( $html, { rows => $rows } );
16 };

17 dance;

18 __DATA__
<!DOCTYPE html>
```
```

```
```
<html>
    <head>

        <title>Sample Database</title>
        <style>
            body {
                background: #66ff33;
            }

            table.coaches {
                border-collapse: collapse;
                background: white;
            }

            table.coaches, table.coaches tr, table.coaches td {
                border: 1px;
                padding: 10px;
            }
        </style>
    </head>
    <body>
        <h1>Contents of the “coaches” Table</h1>

        <table class="coaches">
            <tr>
                <th>ID</th>
                <th>Name</th>
                <th>Team</th>
                <th>Title</th>
                <th>Start date</th>
            </tr>
```
```