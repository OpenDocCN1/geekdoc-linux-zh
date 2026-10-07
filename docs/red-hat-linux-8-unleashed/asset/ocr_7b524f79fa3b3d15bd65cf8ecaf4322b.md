The first thing that acts on the list is the map operator. It transforms the list into a hash in which the keys are the list elements and the values are the lengths of each element. This is where you put in your code that does the transformation by which you want to sort.
The next operator is the sort function, which sorts the list by the values.

Finally, the hash is transformed back into an array by extracting its keys. The array is now in the desired order.

# Command Line Processing

Perl is great at parsing the output of various programs. This is a task for which many people use tools such as awk and sed. Perl gives you a larger vocabulary for performing tasks. The following example is very simple, but illustrates how you might use Perl chop some output and do something with it. In the example, Perl is used to list only files that are larger than 10KB:

```
$ ls -la | perl -nae 'print \$F[8] is \$F[4]\n' if \$F[4] > 10000;
```

The -n switch indicates that I want the Perl code run for each line of the output. The -a switch automatically splits the output into the @F array. The -e switch indicates that the Perl code is going to follow the command line. (Refer to the “Switches” section earlier in this chapter for more information.)

Red Hat and Linux Commands
You'll use these commands and tools when using Perl with Red Hat Linux:
ap—Filter used to translate awk scripts into Perl
find2perl—A utility to create Perl code from command lines using the find command
pcregrep—A utility to search data using Perl-compatible regular expressions
perlcc—A compiler for Perl programs
perldoc—A utility used to read Perl documentation
s2p—A filter used to translate scripts into Perl
vi—The vi (actually vim) text editor

# Reference

The first place to look is the Perl documentation and Linux man pages.
Perl, all of its documentation, and millions of Perl programs are all available free on the Internet. A number of Usenet newsgroups are also devoted to Perl, as well as shelves of books and a quarterly journal.