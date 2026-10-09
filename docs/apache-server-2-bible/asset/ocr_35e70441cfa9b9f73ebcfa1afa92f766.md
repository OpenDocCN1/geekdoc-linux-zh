```
```
print STDERR "Can not connect to $dataSource \n";
print STDERR "DB2 Server Error: $DBI::errstr \n";
}

}
my prepare_statement (
    my $dbh = shift;

    my $statement = "SELECT myfield from mytable where ID = ?";
    $sth = $dbh->prepare($statement);
}
```
```
sub handle (
    my $r = shift;

    if ($APP_RUN_COUNT++ == 0) {
        init();
        prepare_statement();
    }

    my $q = new CGI;
    my $id = $q->param('id');
    my $rv = $sth->execute($id);
    if (! $rv ) {
        # No record found. Do something
    }

    while ( my @fields = $sth->fetchrow_array){
        print STDOUT "ID $id shows: ", join(',', @fields), "<br>";
    }

    $sth->finish;
}
```
```

Here the handler method calls `init()` and `prepare_statement()` routines to create global database and statement handles once for the entire life cycle of the child-server process. This makes the script much more efficient than the previous version.