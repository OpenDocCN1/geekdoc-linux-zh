The first thing edit_member.pl needs to know is the names of the columns in the member table and whether they can be assigned NULL values. The latter property will be used when a column value is cleared (we'll assign the column NULL if the column can take NULL values and the empty string otherwise). The required information is available in the COLUMNS table of the INFORMATION_SCHEMA database:

```
my @col_name = ();   # array of column names
my %nullable = ();   # column nullability, keyed on column name
# get member table column names
my $sth = $dbh->prepare (qq{
    SELECT COLUMN_NAME, UPPER(IS_NULLABLE)
    FROM INFORMATION_SCHEMA.COLUMNS
    WHERE TABLE_SCHEMA = ? AND TABLE_NAME = ?
});
$sth->execute ('s&mpdb', 'member');
while (my ($col_name, $is_nullable) = $sth->fetchrow_array ())
{
  push (@col_name, $col_name);
  $nullable{$col_name} = ($is_nullable eq "YES");
}
```

Using the column information, the script produces an array containing the column names in order, and a hash keyed by column name that indicates whether each column is *nullable*. Then edit_member.pl enters its main loop:

```
if (@ARGV == 0) { # if no arguments were given, create a new entry
{

# pass reference to array of column names
new_member (\@col_name);
}
else        # otherwise edit entries using arguments as member IDs
{

# save @ARGV, and then empty it so that when the script reads from
# STDIN, it doesn't interpret @ARGV contents as input filenames
my @id = @ARGV;
@ARGV = ();
# for each ID value, look up the entry, and then edit it
while (my $id = shift (@id))
{

$sth = $dbh->prepare (qq{
    SELECT * FROM member WHERE member_id = ?
});
$sth->execute ($id);
my $entry_ref = $sth->fetchrow_hashref ();
$sth->finish ();
if (!$entry_ref)
{
 warn 'No member exists with member ID = $id\n';
```