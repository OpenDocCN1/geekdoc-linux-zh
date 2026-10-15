
To have Perl examine your system and then download and install a large number of modules, use the install keyword, specify Bundle at the prompt, and then press Enter like this:

```
cpan> install Bundle::CPAN
```

To download a desired module (using the example in Listing 23.6), use the get keyword like so:

```
cpan> get Mail::Sendmail
```

The source for the module will be downloaded into the .cpan directory. You can then build and install the module using the install keyword, like this:

```
cpan> install Mail::Sendmail
```

The entire process of retrieving, building, and installing a module can also be accomplished at the command line by using Perl’s option like this:

```
# perl -MCPAN -e 'install Mail::Sendmail'
```

Note also that the @ sign did not need to be escaped within single quotation marks (''). Perl does not interpolate (evaluate variables) within single quotation marks, but does within double quotation marks and here strings (similar to << shell operations).

## Purging Logs

Many programs maintain some variety of logs. Often, much of the information in the logs is redundant or just useless. The program shown in Listing 23.7 removes all lines from a file that contain a particular word or phrase, so lines that you know are not important can be purged. For example, you might want to remove all the lines in the Apache error log that originate with your test client machine because you know those error messages were produced during testing.

### LISTING 23.7 Purging Log Files

```
#!/usr/bin/perl
# Be careful using this program!
# This will remove all lines that contain a given word
# Usage: remove <word> <file>
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
}
# End for
close FILE;
} else {
  print "Usage: remove <word> <file>\n";
} # End if...else
```

The code uses a few idiomatic Perl expressions to keep it brief. It reads the file into an array using the `<FILE>` notation; it then writes the lines back out to the file unless they match the pattern given on the command line.

The die function kills program operation and displays an error message if the open statements fail. `$!` in the error message, as mentioned in the section on special variables, is the error message returned by the operating system. It will likely be something like ‘file not found’ or ‘permission denied.’

## Posting to Usenet

If some portion of your job requires periodic postings to Usenet—a FAQ listing, for example—the following Perl program can automate the process for you. In the sample code, the posted text is read in from a text file, but your input can come from anywhere.

The program shown in Listing 23.8 uses the Net::NNTP module, which is a standard part of the Perl distribution. You can find more documentation on the Net::NNTP module by typing `perldoc Net::NNTP` at the command line.

### LISTING 23.8 Posting an Article to Usenet

```
#!/usr/bin/perl
# load the post data into @post
open (POST, 'post.file');
@post = <POST>;
close POST;
# import the NNTP module
use Net::NNTP;
$NNTPHost = 'news';
# attempt to connect to the remote host;
# print an error message on failure
$nntp = Net::NNTP->new($NNTPHost)
  or die "Cannot contact $NNTPHost: $!";
# $nntp->debug(1);
$nntp->post()
  or die "Could not post article: $!";
# send the header of the post
$nntp->datasend("Newsgroups: news.announce\n");
$nntp->datasend('Subject: FAQ - Frequently Asked Questions\n');
$nntp->datasend('From: ADMIN <root>\n');
$nntp->datasend("\n");
# for each line in the @post array, send it
for (@post) {
    $nntp->datasend($_);
} # End for
$nntp->quit;
```

## One-Liners

One medium in which Perl excels is the one-liner. Folks go to great lengths to reduce tasks to one line of Perl code. Perl has the rather undeserved reputation of being unreadable. The fact is that you can write unreadable code in any language. Perl allows for more than one way to do something, and this leads rather naturally to people trying to find the most arcane way to do things.

Named for Randal Schwartz, a Schwartzian Transform is a way of sorting an array by something that is not obvious. The sort function sorts arrays alphabetically; that is pretty obvious. What if you want to sort an array of strings alphabetically by the third word? Perhaps you want something more useful, such as sorting a list of files by file size? A Schwartzian Transform creates a new list that contains the information that you want to sort by, referencing the first list. You then sort the new list and use it to figure out the order that the first list should be in. Here’s a simple example that sorts a list of strings by length:

```
@sorted_by_length =
map { $_ => [0] }          # Extract original list
sort { $a->[1] <=> $b->[1] }  # Sort by the transformed value
map { [$_ , length($_)] }     # Map to a list of element lengths
@list;
```

Because each operator acts on the thing immediately to the right of it, it helps to read this from right to left (or bottom to top, the way it is written here).

The first thing that acts on the list is the map operator. It transforms the list into a hash in which the keys are the list elements and the values are the lengths of each element. This is where you put in your code that does the transformation by which you want to sort.

The next operator is the sort function, which sorts the list by the values.

Finally, the hash is transformed back into an array by extracting its keys. The array is now in the desired order.

## Command-Line Processing

Perl is great at parsing the output of various programs. This is a task for which many people use tools such as awk and sed. Perl gives you a larger vocabulary for performing these tasks. The following example is very simple, but illustrates how you might use Perl to chop up some output and do something with it. In the example, Perl is used to list only those files that are larger than 10KB:
