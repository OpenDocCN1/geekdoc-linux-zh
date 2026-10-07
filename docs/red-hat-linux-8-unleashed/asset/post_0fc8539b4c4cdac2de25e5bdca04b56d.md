
Once you've installed a module from CPAN (or written one of your own), you can load
that module into memory where you can use it with the function:

```perl
use Time::CTime;
```

use looks in the directories listed in the variable @INC for the module. In example, use
looks for a directory called Time, which contains a file called CTime.pm, which in turn is
assumed to contain a package Time::CTime. The distribution of each module should
contain documentation on using that module.

For a list of all the standard Perl modules (those that come with Perl when you install it),
see permodlib in the Perl documentation. You can read this document by typing
perldoc permodlib at the command prompt.

## Code Examples

Over the last few years, many people have picked up the notion that Perl is a CGI
language, as though it wasn't good for anything else. Nothing could be further from the
truth. You can use Perl in every aspect of your system administration and as a building
block in whatever applications you're planning to run on your shiny new Linux system.

The following sections contain a few examples of things you might want to do with Perl.

## Sending Mail

There are several ways to get Perl to send email. One method that you use frequently is
open a pipe to the sendmail command and sending data to it (shown in Listing 23.5).
Another method is using the Mail::Sendmail module (available through CPAN or directly
at http://www.cpan.org/authors/id/M/MI/MIVKOVIC/), which uses socket connections
direct to send mail (as shown in Listing 23.6). The latter method is faster because it
didn't have to launch an external process.

## LISTING 23.5 Sending Mail Using Mail

```perl
#!/usr/bin/perl
open (MAIL, "/usr/bin/sendmail -t"); # Use -t to protect from users
print MAIL <<EndMail:
To: dipitts@mk.net
From: rbowen@mk.net
Subject: Email notification

David,
Sending email from Perl is easy!
Rich
.EndMail
close MAIL;
```

## NOTE

Note that the @ sign in the email addresses must be escaped so that Perl doesn't try to evaluate
an array of that name.

The syntax used to print the mail message is called a here document. The syntax is as follows:
print <<EndText;

```
...
EndText;
```

The EndText value must be identical at the beginning and at the end of the block, including any
whitespace.

## LISTING 23.6 Sending Mail Using the Mail::Sendmail Module

```perl
use Mail::Sendmail;
%mail = ( 'To' => 'dpitts@mk.net',
  'From' => 'rbowen@mk.net',
  'Subject' => 'Email notification',
  'Message' => 'Sending email from Perl is easy!',
);
sendmail(%mail);
```

Perl ignores the comma after the last element in the hash. It's convenient to leave it there;
if you want to add items to the hash, you don't need to add the comma. This is purely a
style decision.

### Using Perl to Install a CPAN Module

You can use Perl to interactively download and install a Perl module from the CPAN archives by
using the -M and -c commands. Start the process by using a Perl like this:

```bash
# perl -MCPAN -e shell
```

After you press Enter, you will see some introductory information, and will be asked to choose an
initial or manual configuration, which is required before any download or install
takes place. Type no and press Enter to have Perl automatically configure for the download and install
process; or if desired, simply press Enter to manually configure for downloading and installation.
If you use manual configuration, you will be asked a series of questions regarding paths, caching,
terminal settings, program locations, and so on. Settings will be saved in a directory named
cpan in current directory.

When finished, you'll see the CPAN prompt:
cpan>

## CHAPTER 23 Using Perl

To have Perl examine your system and download and install a large number of modules, use the install keyword, specify Bundle at the prompt, and then press Enter like this:

```bash
cpan install Bundle::CPAN
```

To download a desired module (using the example in Listing 23.6), use the get keyword like so:

```bash
cpan get Mail::Sendmail
```

The source for the module will be downloaded into the .cpan directory. You can then build and install the module using the install keyword, like this: 

```bash
cpan> install Mail::Sendmail
```

The entire process of retrieving, building and installing a module can also be accomplished with the command line using Perl's -e option like this:

```bash
# perl -CPAN -e "install Mail::Sendmail"
```

Note that the @ sign does not need to be escaped within single quotation marks (''). Perl doesn't interpolate (evaluate variables) within single quotation marks, but does within double quotation marks, and here documents.

## Purging Logs

Many programs maintain some variety of logs. Often, much of the information in the logs is redundant or useless. The program shown in Listing 23.7 removes all lines from a file that contain a particular word or phrase, so that those you know are important can be purged. For example, you might want to remove all the lines in the Apache error log that originate from your test client machine because you know.

## LISTING 23.7 Purging Logs

```perl
#!/usr/bin/perl
# This program removes all lines from a file that contain a particular word or phrase
# Usage: purge.pl <file> <word>
($file, $word) = @ARGV;
open(IN, "<", $file) or die "Could not open $file: $!";
open(OUT, ">", "$file.tmp") or die "Could not open file: $!";
while ($line = <IN>) {
  if ($line !~ /$word/) {
    print OUT $line;
  }
}
close(IN);
close(OUT);
rename("$file.tmp", $file);
```

## Posting to Usenet

There are several ways to get Perl to send email. One method that you use frequently is
open a pipe to the sendmail command and sending data to it (shown in Listing 23.5).
Another method is using the Mail::Sendmail module (available through CPAN or directly
at http://www.cpan.org/authors/id/M/MI/MIVKOVIC/), which uses socket connections
direct to send mail (as shown in Listing 23.6). The latter method is faster because it
didn't have to launch an external process.

## LISTING 23.5 Sending Mail Using Mail

```perl
#!/usr/bin/perl
open (MAIL, "/usr/bin/sendmail -t"); # Use -t to protect from users
print MAIL <<EndMail:
To: dipitts@mk.net
From: rbowen@mk.net
Subject: Email notification

David,
Sending email from Perl is easy!
Rich
.EndMail
close MAIL;
```

## NOTE

Note that the @ sign in the email addresses must be escaped so that Perl doesn't try to evaluate
an array of that name.

The syntax used to print the mail message is called a here document. The syntax is as follows:
print <<EndText;

```
...
EndText;
```

The EndText value must be identical at the beginning and at the end of the block, including any
whitespace maintain some variety of logs. Often, much of the information in the logs is redundant or useless. The program shown in Listing 23.7 removes all lines from a file that contain a particular word or phrase, so that those you know are important can be purged. For example, you might want to remove all the lines in the Apache error log that originate from your test client machine because you know.

## LISTING 23.6 Sending Mail Using the Mail::Sendmail Module

```perl
use Mail::Sendmail;
%mail = ( 'To' => 'dpitts@mk.net',
  'From' => 'rbowen@mk.net',
  'Subject' => 'Email notification',
  'Message' => 'Sending email from Perl is easy!',
);
sendmail(%mail);
```

Perl ignores the comma after the last element in the hash. It's convenient to leave it there;
if you want to add items to the hash, you don't need to add the comma. This is purely a
style decision.

### Using Perl to Install a CPAN Module

You can use Perl to interactively download and install a Perl module from the CPAN archives by
using the -M and -c commands. Start the process by using a Perl like this:

```bash
# perl -MCPAN -e shell
```

After you press Enter, you will see some introductory information, and will be asked to choose an
initial or manual configuration, which is required before any download or install
takes place. Type no and press Enter to have Perl automatically configure for the download and install
process; or if desired, simply press Enter to manually configure for downloading and installation.
If you use manual configuration, you will be asked a series of questions regarding paths, caching,
terminal settings, program locations, and so on. Settings will be saved in a directory named
cpan in current directory.

When finished, you'll see the CPAN prompt:
cpan>

## CHAPTER 23 Using Perl

To have Perl examine your system and download and install a large number of modules, use the install keyword, specify Bundle at the prompt, and then press Enter like this:

```bash
cpan install Bundle::CPAN
```

To download a desired module (using the example in Listing 23.6), use the get keyword like so:

```bash
cpan get Mail::Sendmail
```

The source for the module will be downloaded into the .cpan directory. You can then build and install the module using the install keyword, like this: 

```bash
cpan> install Mail::Sendmail
```

The entire process of retrieving, building and installing a module can also be accomplished with the command line using Perl's -e option like this:

```bash
# perl -CPAN -e "install Mail::Sendmail"
```

Note that the @ sign does not need to be escaped within single quotation marks (''). Perl doesn't interpolate (evaluate variables) within single quotation marks, but does within double quotation marks, and here documents.

## Purging Logs

Many programs maintain some variety of logs. Often, much of the information in the logs is redundant or useless. The program shown in Listing 23.7 removes all lines from a file that contain a particular word or phrase, so that those you know are important can be purged. For example, you might want to remove all the lines in the Apache error log that originate from your test client machine because you know.

## LISTING 23.7 Purging Logs

```perl
#!/usr/bin/perl
# This program removes all lines from a file that contain a particular word or phrase
# Usage: purge.pl <file> <word>
($file, $word) = @ARGV;
open(IN, "<", $file) or die "Could not open $file: $!";
open(OUT, ">", "$file.tmp") or die "Could not open file: $!";
while ($line = <IN>) {
  if ($line !~ /$word/) {
    print OUT $line;
  }
}
close(IN);
close(OUT);
rename("$file.tmp", $file);
```

## Posting to Usenet

There are several ways to get Perl to send email. One method that you use frequently is
open a pipe to the sendmail command and sending data to it (shown in Listing 23.5).
Another method is using the Mail::Sendmail module (available through CPAN or directly
at http://www.cpan.org/authors/id/M/MI/MIVKOVIC/), which uses socket connections
direct to send mail (as shown in Listing 23.6). The latter method is faster because it
didn't have to launch an external process.

## LISTING 23.5 Sending Mail Using Mail

```perl
#!/usr/bin/perl
open (MAIL, "/usr/bin/sendmail -t"); # Use -t to protect from users
print MAIL <<EndMail:
To: dipitts@mk.net
From: rbowen@mk.net
Subject: Email notification

David,
Sending email from Perl is easy!
Rich
.
EndMail
close MAIL;
```

## NOTE

Note that the @ sign in the email addresses must be escaped so that Perl doesn't try to evaluate
an array of that name.

The syntax used to print the mail message is called a here document. The syntax is as follows:
print <<EndText;

```
...
EndText;
```

The EndText value must be identical at the beginning and at the end of the block, including any
whitespace.

## LISTING 23.6 Sending Mail Using the Mail::Sendmail Module

```perl
use Mail::Sendmail;
%mail = ( 'To' => 'dpitts@mk.net',
  'From' => 'rbowen@mk.net',
  'Subject' => 'Email notification',
  'Message' => 'Sending email from Perl is easy!',
);
sendmail(%mail);
```

Perl ignores the comma after the last element in the hash. It's convenient to leave it there;
if you want to add items to the hash, you don't need to add the comma. This is purely a
style decision.

### Using Perl to Install a CPAN Module

You can use Perl to interactively download and install a Perl module from the CPAN archives by
using the -M and -c commands. Start the process by using a Perl like this:

```bash
# perl -MCPAN -e shell
```

After you press Enter, you will see some introductory information, and will be asked to choose an
initial or manual configuration, which is required before any download or install
takes place. Type no and press Enter to have Perl automatically configure for the download and install
process; or if desired, simply press Enter to manually configure for downloading and installation.
If you use manual configuration, you will be asked a series of questions regarding paths, caching,
terminal settings, program locations, and so on. Settings will be saved in a directory named
cpan in current directory.

When finished, you'll see the CPAN prompt:
cpcan>

## CHAPTER 23 Using Perl

To have Perl examine your system and download and install a large number of modules, use the install keyword, specify Bundle at the prompt, and then press Enter like this:

```bash
cpan install Bundle::CPAN
```

To download a desired module (using the example in Listing 23.6), use the get keyword like so:

```bash
cpan get Mail::Sendmail
```

The source for the module will be downloaded into the .cpan directory. You can then build and install the module using the install keyword, like this: 

```bash
cpan> install Mail::Sendmail
```

The entire process of retrieving, building and installing a module can also be accomplished with the command line using Perl's -e option like this:

```bash
# perl -CPAN -e "install Mail::Sendmail"
```

Note that the @ sign does not need to be escaped within single quotation marks (''). Perl doesn't interpolate (evaluate variables) within single quotation marks, but does within double quotation marks, and here documents.

## Purging Logs

Many programs maintain some variety of logs. Often, much of the information in the logs is redundant or useless. The program shown in Listing 23.7 removes all lines from a file that contain a particular word or phrase, so that those you know are important can be purged. For example, you might want to remove all the lines in the Apache error log that originate from your test client machine because you know.

## LISTING 23.7 Purging Logs

```perl
#!/usr/bin/perl
# This program removes all lines from a file that contain a particular word or phrase
# Usage: purge.pl <file> <word>
($file, $word) = @ARGV;
open(IN, "<", $file) or die "Could not open $file: $!";
open(OUT, ">", "$file.tmp") or die "Could not open file: $!";
while ($line = <IN>) {
  if ($line !~ /$word/) {
    print OUT $line;
  }
}
close(IN);
close(OUT);
rename("$file.tmp", $file);
```

## Posting to Usenet

There are several ways to get Perl to send email. One method that you use frequently is
open a pipe to the sendmail command and sending data to it (shown in Listing 23.5).
Another method is using the Mail::Sendmail module (available through CPAN or directly
at http://www.cpan.org/authors/id/M/MI/MIVKOVIC/), which uses socket connections
direct to send mail (as shown in Listing 23.6). The latter method is faster because it
didn't have to launch an external process.

## LISTING 23.5 Sending Mail Using Mail

```perl
#!/usr/bin/perl
open (MAIL, "/usr/bin/sendmail -t"); # Use -t to protect from users
print MAIL <<EndMail:
To: dipitts@mk.net
From: rbowen@mk.net
Subject: Email notification

David,
Sending email from Perl is easy!
Rich
.
EndMail
close MAIL;
```

## NOTE

Note that the @ sign in the email addresses must be escaped so that Perl doesn't try to evaluate
an array of that name.

The syntax used to print the mail message is called a here document. The syntax is as follows:
print <<EndText;

```
...
EndText;
```

The EndText value must be identical at the beginning and at the end of the block, including any
whitespace.

## LISTING 23.6 Sending Mail Using the Mail::Sendmail Module

```perl
use Mail::Sendmail;
%mail = ( 'To' => 'dpitts@mk.net',
  'From' => 'rbowen@mk.net',
  'Subject' => 'Email notification',
  'Message' => 'Sending email from Perl is easy!',
);
sendmail(%mail);
```

Perl ignores the comma after the last element in the hash. It's convenient to leave it there;
if you want to add items to the hash, you don't need to add the comma. This is purely a
style decision.

## One-Liners

One medium in which Perl excels is the one-liner. Folks go to great lengths to reduce tasks to one line. Perl has the undeserved reputation of being unreadable. The fact is that you can write unreadable code in any language. Perl allows for more than one way to do, and this leads naturally to people trying to find the most arcane way to do it.

> TIP
Because you can do something isn't a particularly good reason for doing it. For example, it could be convenient to write some lengthy pieces of Perl code for something that could be done in one line, just for the sake of readability, and could save time later. It can be irritating to go back to a piece of code reduced to one line for efficiency, but then later on to spend 30 minutes to figure out what it does. Document your Perl scripts for readability. Use comments liberally because they'll help you (or your co-workers who get to maintain your code) in the future.

### Schwartz Transform

Named for Randal Schwartz, a Schwartzian Transform is a way of sorting an array by something that isn't obvious. The sort function sorts arrays alphabetically; that's pretty obvious. If you want to sort an array of strings alphabetically by the third word? Perhaps you want something more useful, like sorting a list of files by file size? A Schwartzian Transform creates a new list that contains the information you want to sort by, referencing the first list. You then sort the new list and use it to figure out the order that the first list should be. Here's a simple example that sorts a list of strings by length:

```perl
@sorted_by_length =
map { $_ => [0] } # Extract original list
sort { $a->[1] <= $b->[1] } # Sort by the transformed value
map { [_$, length($)] } # Map to a list of element elements
@list;
```
