
				}

				# read and display query result
				my $matches = 0;
				while ($my $ary = $sth->fetchrow_arrayref ())
				{
					# print newline before 2nd and subsequent entries
					print "\n" if ++$count > 1;
					foreach ($my $i = 0; $i < $sth->(NUM_OF_FIELDS); $i++)
					{
						# print label
						printf "%-*s", $label_wid+1, $label[$i] . ':';
						# print value, if there is one
						print "  $ary[$i]" if defined ($ary[$i]);
						print "\n";
					}
					++$matches;
				}
				print "\nNo match was found for \"$arg\"\n" if $matches == 0;
				}

The purpose of show_member.pl is to show the entire contents of an entry, no matter what the fields are. By using SELECT * to retrieve all the columns and the NAME attribute to find out what they are, this script works without modification even if columns are added to or dropped from the member table.

If you just want to know what columns a table contains without retrieving any rows, you can issue this statement:

```sql
SELECT * FROM tbl_name WHERE FALSE
```

The WHERE FALSE clause is false for all rows, so executing the statement has the effect of generating column metadata but returning no rows. After invoking prepare() and execute() in the usual way for the statement, you can get the column names from @{$sth->{NAME}}. Be aware that although this little trick of using an “empty” query works for MySQL, it's not portable and may not work for other database systems.

For more information on the attributes provided by DBI and by DBD::mysql, see Appendix H (online). It's up to you to determine whether you want to strive for portability by avoiding MySQL-specific attributes, or take advantage of them at the cost of portability.

## 8.2.12 Performing Transactions

One way to perform transactions in a DBI script is to issue explicit SET AUTOCOMMIT, START TRANSACTION, COMMIT, and ROLLBACK statements. (Section 2.13, “Performing Transactions,” describes these statements.) However, DBI provides its own abstraction for performing transactional operations. This abstraction is expressed in terms of DBI methods and attributes, and takes care of issuing the proper transaction-related SQL statements for you automatically. It's also portable to other database systems that support transactions, whereas the SQL statements may not be.

To use the DBI transaction mechanism, these requirements must be satisfied:

- Your MySQL server must support at least one transaction-safe storage engine such as InnoDB or Falcon. Section 2.6.1.1, “Checking Which Storage Engines Are Available,” describes how to determine whether this is true.
- Your application must use tables that are of a transaction-safe type. If they are not, use `ALTER TABLE` to change their type. For example, to change a given table `tbl_name` to be an InnoDB table, use this statement:

```sql
ALTER TABLE tbl_name ENGINE = InnoDB;
```

Assuming that those requirements are satisfied, use this general procedure for transactional processing in DBI:

1. Disable (or temporarily suspend) autocommit mode so that SQL statements won't be committed until you commit them yourself.
2. Issue the statements that are part of a transaction, but do so within an `eval` block that executes with `RaiseError` enabled and `PrintError` disabled so that any errors will terminate the block without printing errors. If the block executes successfully, the last operation within it should be to invoke `commit()` to commit the transaction.
3. When the `eval` block finishes, check its termination status. If an error occurred, invoke `rollback()` to cancel the transaction and report the error if that's appropriate.
4. Restore the autocommit mode and error-handling attributes as necessary.

The following example shows how to implement this approach. It's based on a scenario from Chapter 2, “Using SQL to Manage Data,” that showed how to issue transaction-related statements manually from the `mysql` client. The scenario is one in which you discover that you've mistakenly mixed up two scores for students in the `score` table and need to switch them: Student 8 has been given a score of 18, student 9 has been given a score of 13, and the scores should be the other way around. The two `UPDATE` statements needed to correct this problem are as follows:

```sql
UPDATE score SET score = 13 WHERE event_id = 5 AND student_id = 8;
UPDATE score SET score = 18 WHERE event_id = 5 AND student_id = 9;
```

You want to update both rows with the correct scores, but both updates must succeed as a unit. The example in the earlier chapter surrounded the updates by explicit SQL statements for setting the autocommit mode, committing, and rolling back. Within a Perl script that uses the DBI transaction mechanism, performing the updates as follows:

```perl
my $orig_re = $dbh->(RaiseError);  # save error-handling attributes
my $orig_pe = $dbh->(PrintError);
my $orig_ac = $dbh->(AutoCommit);  # save auto-commit mode

$dbh->(RaiseError) = 1;             # cause errors to raise exceptions
$dbh->(PrintError) = 0;             # but suppress error messages
$dbh->(AutoCommit) = 0;         # don't commit until we say so

eval
{
    # issue the statements that are part of the transaction
    my $sth = $dbh->prepare (qq{
        UPDATE score SET score = ?
        WHERE event_id = ? AND student_id = ?
        });
    $sth->execute (13, 5, 8);
    $sth->execute (18, 5, 9);
    $dbh->commit();            # commit the transaction
};
if ($@)                       # did the transaction fail?
{
    print "A transaction error occurred: $@\n";
    # roll back, but use eval to trap rollback failure
    eval { $dbh->rollback (); }
}

$dbh->(AutoCommit) = $orig_ac;    # restore auto-commit mode
$dbh->(RaiseError) = $orig_re;    # restore error-handling attributes
$dbh->(PrintError) = $orig_pe;
```

The eval block does the work of performing the transaction, and its termination status is available in the $@ variable. If the UPDATE statements and the commit() method execute without error, $@ will be empty. If an error occurs, the eval block fails and $@ holds the error message. In that case, the code prints the message, and then cancels the transaction by invoking rollback(). (The rollback operation is placed within its own eval block to prevent it from terminating the script if it fails.)

In this chapter, DBI scripts generally use an error-handling mode in which RaiseError is enabled and PrintError is disabled. This means that they already will have the values required for performing transactions, and thus it really wouldn't have been necessary to save, set, and restore those attributes as shown in the example. However, doing so is an approach that will work even for circumstances under which you're not sure in advance what the error-handling attributes might be.

## 8.3 Putting DBI to Work

At this point you've seen a number of the concepts involved in DBI programming, so let's move on to some of the things we wanted to be able to do with our sample database. Our goals were outlined initially in Chapter 1. Those that we'll tackle by writing DBI scripts in this chapter are listed here:

- For the grade-keeping project, we want to be able to retrieve scores for any given quiz or test.
- For the Historical League, we want to do the following:
  - Produce the member directory in different formats. We want a names-only list for use in the program distributed at the League's annual meeting, and in a format we can use for generating the printed directory.
  - Find League members that need to renew their memberships soon, and then send them email to let them know about it.
  - Edit member entries. (We'll need to update their expiration dates when they renew their memberships, after all.)
  - Find members that share a common interest.
  - Put the directory online.

For some of these tasks, we'll write scripts that run from the command line. For the others, we'll create scripts in Section 8.4, “Using DBI in Web Applications,” that you can use in conjunction with your Web server. At the end of the chapter, we'll still have a number of goals left to accomplish. We'll finish up those that remain in Chapter 9, “Writing MySQL Programs Using PHP.”

### 8.3.1 Generating the Historical League Directory

One of our goals is to be able to produce information from the Historical League directory in different formats. The simplest format to be generated is a list of member names for the printed program distributed to attendees at the League's annual meeting. The format can be a simple plain text listing. It will become part of the larger document used to create the meeting program, so all we need is something that can be pasted into that document.

For the printed member directory, a better representation than plain text is needed because we want something nicely formatted. A reasonable choice here is RTF (Rich Text Format), a format developed by Microsoft that is understood by many word processors. Word is one such program, of course, but many others such as OpenOffice understand it as well. Different word processors support RTF to varying degrees, but we'll use a basic subset of the full RTF specification that should be understandable by any program that is RTF-aware. For example, on Mac OS X, the TextEdit editor and the Safari Web browser can read the RTF output that we'll generate.

The procedures for generating the annual meeting list (plain text) and RTF directory formats are essentially the same: Issue a query to retrieve the entries, and then run a loop that fetches and formats each entry. Given that basic similarity, it would be nice to avoid writing separate scripts for each format. To that end, let's write a single script, gen_dir.pl, that can generate different types of output. We'll structure the script as follows:

- Before writing out member entries, perform any initialization that might be necessary for the output format. No special initialization is necessary for the plain text member list, but we'll need to write out some initial control language for the RTF version.
