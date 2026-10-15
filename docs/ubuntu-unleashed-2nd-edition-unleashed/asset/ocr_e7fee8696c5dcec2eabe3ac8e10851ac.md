Because each operator acts on the thing immediately to the right of it, it helps to read this from right to left (or bottom to top, the way it is written here).

The first thing that acts on the list is the map operator. It transforms the list into a hash in which the keys are the list elements and the values are the lengths of each element. This is where you put in your code that does the transformation by which you want to sort.

The next operator is the sort function, which sorts the list by the values.

Finally, the hash is transformed back into an array by extracting its keys. The array is now in the desired order.

# Command-Line Processing

Perl is great at parsing the output of various programs. This is a task for which many people use tools such as awk and sed. Perl gives you a larger vocabulary for performing these tasks. The following example is very simple, but it illustrates how you might use Perl to chop up some output and do something with it. In the example, Perl is used to list only those files that are larger than 10KB:

```
$ ls -la | perl -nae 'print "$F[8] is $F[4]\n" if $F[4] > 10000;'
```

The -n switch indicates that I want the Perl code run for each line of the output. The -a switch automatically splits the output into the @F array. The -e switch indicates that the Perl code is going to follow on the command line.

# Related Ubuntu and Linux Commands

You will use these commands and tools when using Perl with Linux:

+   - `a2p`—A filter used to translate awk scripts into Perl
+   - `find2perl`—A utility used to create Perl code from command lines using the find command
+   - `pcregrep`—A utility used to search data using Perl-compatible regular expressions
+   - `perlc`—A compiler for Perl programs
+   - `perldoc`—A Perl utility used to read Perl documentation
+   - `s2p`—A filter used to translate sed scripts into Perl
+   - `vi`—The vi (actually vim) text editor

# Reference

The first place to look is in the Perl documentation and Linux man pages.

Perl, all of its documentation, and millions of lines of Perl programs are all available free on the Internet. A number of Usenet newsgroups are also devoted to Perl, as are shelves of books and a quarterly journal.