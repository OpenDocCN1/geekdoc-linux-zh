error log that originate with your test client machine because you know those error messages were produced during testing.

# LISTING 29.7 Purging Log Files

```
#!/usr/bin/perl
#		Be careful using this program!!
#		This will remove all lines that contain a given word
#		Usage: remove <word> <file>
$word=$ARGV[0];
$file=$ARGV[1];
if ($file) {
	# Open file for reading
	open (FILE, "$file") or die "Could not open file: $!";	@lines=<FILE>;
	close FILE;
	# Open file for writing
	open (FILE, ">$file") or die "Could not open file for writing: $!";
	for (@lines) {
		print FILE unless /$word/;
	} # End for
	close FILE;
} else {
	print "Usage: remove <word> <file>\n";
} # End if...else
```

The code uses a few idiomatic Perl expressions to keep it brief. It reads the file into an array using the `<FILE>` notation; it then writes the lines back out to the file unless they match the pattern given on the command line.

The die function kills program operation and displays an error message if the open statements fail. $! in the error message, as mentioned in the section on special variables, is the error message returned by the operating system. It will likely be something like 'file not found' or 'permission denied'.

# Posting to Usenet

If some portion of your job requires periodic postings to Usenet—a FAQ listing, for example—the following Perl program can automate the process for you. In the sample code, the posted text is read in from a text file, but your input can come from anywhere.

The program shown in Listing 29.8 uses the Net::NNTP module, which is a standard part of the Perl distribution. You can find more documentation on the Net::NNTP module by typing `perldoc Net::NNTP` at the command line.