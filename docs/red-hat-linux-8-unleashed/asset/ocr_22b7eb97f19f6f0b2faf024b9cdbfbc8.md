If you're interested in the details, you can get more information using the regex (5)
section of the manual.

Although replacing one string with another might seem a rather trivial task, the code
required to do the same thing in another language (for example, C) is rather daunting,
unless supported by additional subroutines from external libraries.

# Access to the Shell

Perl is useful for Administrative functions because it has access to the shell. That means
Perl can perform for any process you might ordinarily perform by typing commands
to the shell. To run Linux commands in your Perl programs use the syntax. For
example, the code in Listing 23.4 prints a directory listing.

LISTING 23.4 Using Backticks to Access the Shell

```
$Scurr = `pwd`;
@list = ls -la;
print 'Listing for $Scurr_dir\n';
foreach $file (@list) {
    print "$file"
}
```

> NOTE
The `` notation uses the backtick found above the Tab key (on most keyboards), not the single
quotation mark.

You can also use the Shell module to access the shell. Shell is one of the standard
modules that you use with Perl; it allows creation and use of a shell-like command line.
Look at the following code for example:

```
use Shell qw(cp);
cp ("/home/httpd/logs/access.log", "/tmp/httpd.log");
```

This code looks like it's actually importing the command-line functions directly into Perl.
Although it's not really happening, you can pretend that the code is similar to a
command line and use this approach in your Perl programs.

A third method of accessing the shell is via the system function call:

```
$rc = 0xffffffff & system('cp /home/httpd/logs/access.log /tmp/httpd.log');
if ($rc == 0) {
    print "system cp succeeded\n";
}
```