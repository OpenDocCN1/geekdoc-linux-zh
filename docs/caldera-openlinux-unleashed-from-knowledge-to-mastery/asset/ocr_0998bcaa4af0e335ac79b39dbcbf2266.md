# LISTING 32.6 Sending Mail Using the Mail::Sendmail Module

```
```
use Mail::Sendmail;
%mail = ('To' => 'dpitts@mik.net',
         'From' => 'rbowen@mik.net',
         'Subject' => 'Email notification',
         'Message' => 'Sending email from Perl is easy!');
sendmail(%mail);
```
```

Perl ignores the comma after the last element in the hash. It is convenient to leave it there; if you want to add items to the hash, you do not need to add the comma. This is purely a style decision.

Note also that the @ sign did not need to be escaped within single quotation marks (' '). Perl does not *interpolate* (evaluate variables) within single quotation marks, but does within double quotation marks and here documents.

# Purging Logs

Many programs maintain some variety of logs. Often, much of the information in the logs is redundant or just useless. The program shown in Listing 32.7 removes all lines from a file that contain a particular word or phrase, so that lines you know are not important can be purged. For example, one might want to remove all the lines in the Apache error log that originate with your test client machine because you know that these error messages were produced during testing.

# LISTING 32.7 Purging Log Files

```
```
#!/usr/bin/perl
#    Be careful using this program!!
#       This will remove all lines that contain a given word
#       Usage:  remove <word> <file>
$word=$ARGV[0];
$file=$ARGV[1];
if ($file) {
    # Open file for reading
    open (FILE, "$file") or die "Could not open file: $!";    @lines=<FILE>;
    close FILE;
    # Open file for writing
    open (FILE, ">$file") or die "Could not open file for writing: $!";
    for (@lines) {
        print FILE unless /$word/;
    } # End for
    close FILE;
} else {
    print "Usage:  remove <word> <file>\n";
} # End if...else
```
```