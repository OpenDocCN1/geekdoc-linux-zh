The function `read_file()` reads the contents of a file (assumed to be open already) and looks at the first field of each line. (If we feed the output of `renewal_renewal.pl` to `renewal_notify.pl`, each line has several fields, but we want to look only at the first one, which will contain a member ID number.)

```
sub read_file
(
    my $fh = shift;    # handle to already-opened file
    my $arg;

    while (defined ($arg = <$fh>)) {
        # strip off everything past column 1, including newline
        $arg =~ s/\b.*/|/g;
        # interpret argument, without filename recursion
        interpret_argument ($arg, 0);
    }
)
```

The `interpret_argument()` function classifies each argument to determine whether it’s an ID number, an email address, or a filename. For ID numbers and email addresses, it looks up the appropriate member entry and passes it to `notify_member()`. We have to be careful with members specified by email address. It’s possible that two members have the same address (for example, a husband and wife), and we don’t want to send a message to someone to whom it doesn’t apply. To avoid this, we look up the member ID corresponding to an email address to make sure that there is exactly one. If the address matches more than one ID number, it’s ambiguous and we ignore it after printing a warning. If an argument doesn’t look like an ID number or email address, it’s taken to be the name of a file to read for further input. We have to be careful here, too— we don’t want to read a file if we’re already reading a file, to avoid the possibility of an infinite loop:

```
sub interpret_argument
(
    my ($arg, $recurse) = @_;

    if ($arg =~ /^(\d+$)/)        # numeric membership ID
    {
        notify_member ($arg);
    }
    elsif ($arg =~ /@/)    # email address
    {
        # get member_id associated with address
        # (there should be exactly one)
        my $stmt = qq( SELECT member_id FROM member WHERE email = ? );
        my $ary_ref = $dbh->selectcol_arrayref ($stmt, undef, $arg);
        if (scalar (@$ary_ref)) == 0) {
```