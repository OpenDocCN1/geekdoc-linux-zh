778

Development Environment

PART V

# ## Command-Line Processing

Perl is great at parsing the output of various programs. This is a task for which many people use tools such as **awk** and **sed**. Perl gives you a larger vocabulary for performing these tasks. The following example is very simple, but it illustrates how you might use Perl to chop up some output and do something with it. In the example, Perl is used to list only those files that are larger than 10 KB.

```
```
ls -la | perl -nae 'print `$_[8] ls $_[4]\n" if $_[4] > 10000;'
```
```

The **-n** switch indicates that I want the Perl code to run for each line of the output. The **-a** switch automatically splits the output into the `@F` array. The **-e** switch indicates that the Perl code is going to follow on the command line. (See “Switches” earlier in this chapter.)

# # Perl-Related Tools

A number of tools are related to Perl or are included with the Perl distribution. The most common of these follow:

+   - **perldoc** Displays Perl documentation
+   - **pod2html** Converts Perl documentation to HTML format
+   - **pod2man** Converts Perl documentation to man (`nroff`/`troff`) format
+   - **a2p** Converts **awk** scripts to Perl
+   - **s2p** Converts **sed** commands to Perl

# # For More Information

The first place to look for more information is in the Perl documentation and Linux man pages.

Perl, all of its documentation, and millions of lines of Perl programs are all available on the Internet for free. There are also a number of Usenet newsgroups devoted to Perl, as well as shelves of books and a quarterly journal.

# ## Books

Even though your local bookstore may have dozens of titles on Perl, the following books are highly recommended. You might also look at the *Camel Critiques* (Tom Christiansen; **http://language.perl.com/critiques/index.html**) for reviews of other Perl books that are available.