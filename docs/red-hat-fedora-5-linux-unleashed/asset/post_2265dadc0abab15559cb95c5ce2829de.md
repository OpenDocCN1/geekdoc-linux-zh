
Named for Randal Schwartz, a *Schwartzian transform* is a way of sorting an array by something that is not obvious. The sort function sorts arrays alphabetically, that is pretty obvious. What if you want to sort an array of strings alphabetically by the third word? Perhaps you want something more useful, such as sorting a list of files by file size? A Schwartzian transform creates a new list that contains the information that you want to sort by, referencing the first list. You then sort the new list and use it to figure out the order that the first list should be in. Here’s a simple example that sorts a list of strings by length:

```perl
@sorted_by_length =
    map { $_->[0] }        # Extract original list
    sort { $a->[1] <=> $b->[1] }  # Sort by the transformed value
    map { [$_, length($_)] }      # Map to a list of element lengths
    @list;
```

Because each operator acts on the thing immediately to the right of it, it helps to read this from right to left (or bottom to top, the way it is written here).

The first thing that acts on the list is the **map** operator. It transforms the list into a hash in which the keys are the list elements and the values are the lengths of each element. This is where you put in your code that does the transformation by which you want to sort.

The next operator is the **sort** function, which sorts the list by the values. Finally, the hash is transformed back into an array by extracting its keys. The array is now in the desired order.

## Command-Line Processing

Perl is great at parsing the output of various programs. This is a task for which many people use tools such as awk and sed. Perl gives you a larger vocabulary for performing these tasks. The following example is very simple, but illustrates how you might use Perl to chop up some output and do something with it. In the example, Perl is used to list only those files that are larger than 10KB:

```bash
$ ls -la | perl -nae 'print "@F[0] is @F[4]\n"  if @F[4] > 10000;'
```

The -n switch indicates that I want the Perl code run for each line of the output. The -a switch automatically splits the output into the @F array. The -e switch indicates that the Perl code is going to follow on the command line.

## Related Perl and Linux Commands

You will use these commands and tools when using Perl with Linux:

- a2p—A filter used to translate awk scripts into Perl
- c1inc2part2—A utility used to create Perl code from command lines using the find command
- pregrep—A utility used to search data using Perl-compatible regular expressions
- perlcc—A compiler for Perl programs
- perldoc—A Perl utility used to read Perl documentation
- s2p—A filter used to translate sed scripts into Perl
- vi (or busybox) text editor

## Reference

The first place to look is in the Perl documentation and Linux man pages.

Perl, all of its documentation, and millions of lines of Perl programs are all available free on the Internet. A number of Usenet newsgroups are also devoted to Perl, as well as shelves of books and a quarterly journal.

## Books

Although your local bookstore might have dozens of titles on Perl, the following are some of the more highly recommended of these. You might also look at the *Camel Critiques* (Tom Christiansen, http://language.perl.com/critiques/index.html) for reviews of other available Perl books.

- *Advanced Perl Programming*, by Shriram Srinivasan, O'Reilly & Associates
- *Sams Teach Yourself Perl in 24 Days, Second Edition*, by Laura Lemay, Sams Publishing
- *Sams Teach Yourself Perl in 24 Hours, Second Edition*, by Clinton Pierce, Sams Publishing
- *Learning Perl, Third Edition*, by Randal L. Schwartz, Tom Phoenix, O'Reilly & Associates
- *Programming Perl, Third Edition*, by Larry Wall, Tom Christiansen, and Jon Orwant, O'Reilly & Associates
- *Effective Perl Programming: Writing Better Programs with Perl*, by Joseph Hall, Addison-Wesley Publishing Company
- *CGI Programming with Perl, Second Edition*, by Gunther Bizniewski, Scott Guelich, Shishir Gundavaram, O'Reilly & Associates
- *Mastering Regular Expressions*, by Jeffrey Friedl, O'Reilly & Associates

## Usenet

Check out the following on Usenet:

- `comp.lang.perl.misc`—Discusses various aspects of the Perl programming language. Make sure that your questions are Perl specific, not generic CGI programming questions. The regulars tend to flame folks who don't know the difference.
- `comp.infosystems.www.authoring.cgi`—Discusses authoring of CGI programs, so much of the discussion is Perl specific. Make sure that your questions are related to CGI programming, not just Perl. The regulars are very particular about staying on topic.

## WWW

Check these sites on the World Wide Web:

- `http://www.perl.com/`—Tom Christiansen maintains the Perl language home page. This is the place to find all sorts of information about Perl, from its history and culture to helpful tips. This is also the place to download the Perl interpreter for your system.
- `http://www.perl.com/CPAN`—This is part of the site just mentioned, but it merits its own mention. CPAN (Comprehensive Perl Archive Network) is the place for you to find modules and programs in Perl. If you write something in Perl that you think is particularly useful, you can make it available to the Perl community here.
- `http://www.perl.com/pub/q/faqs`—Frequently Asked Questions index of common Perl queries; this site offers a handy way to quickly search for answers about Perl.
- `http://learn.perl.org/`—One of the best places to start learning Perl online. If you master Perl, go to `http://jobs.perl.org`.
- `http://www.hwg.org/`—The HTML Writers Guild is a not-for-profit organization dedicated to assisting web developers. One of its services is a plethora of mailing lists. The `hww-servers` mailing list and the `hww-languages` mailing list are great places for asking Perl-related questions.
- `http://www.pm.org/`—The Perl Mongers are local Perl users groups. There might be one in your area. The Perl advocacy site is `http://www.perl.org/`.
- `http://www.tpj.com/`—*The Perl Journal* is "a reader-supported monthly e-zine" devoted to the Perl programming language. *TPJ* is always full of excellent, amusing, and informative articles, and is an invaluable resource to both new and experienced Perl programmers.
- `http://www-106.ibm.com/developerworks/linux/library/l-p101`—A short tutorial about one-line Perl scripts and code.

## Other

Other valuable resources not falling into any of the preceding categories are Perl-related Internet Relay Chat channels. You can usually find several channels available on an IRC server. However, the questions, discussions, and focus of similarly named channels will vary from server to server.

For example, a `#perlhelp` channel is usually for general questions about installing, using, and learning about Perl. A `#perl` channel is generally for more advanced questions, but on some servers beginner questions might be welcomed. You might also find some helpful answers on `#cgi` and `#nntp` channels. Browse to `http://perl-begin.berlios.de/irc/` for a list of servers.

# CHAPTER 31: Working with Python

## IN THIS CHAPTER

- Python on Linux
- The Basics of Python
- Functions
- Object Orientation
- The Standard Library and the Vaults of Parnassus
- Reference

As PHP has come to dominate the world of web scripting, Python is increasingly dominating the domain of command-line scripting. Python’s precise and clean syntax makes it one of the easiest languages to learn, and it allows programmers to code more quickly and spend less time maintaining their code. Although PHP is fundamentally similar to Java and Perl, Python is closer to C and Modula-3, and so it might look unfamiliar at first.

Most of the other languages have a group of developers at their cores, but Python has Guido van Rossum—creator, father, and Benevolent Dictator For Life (BDFL). Although Guido spends less time working on Python now, he still essentially has the right to veto changes to the language, which has enabled it to remain consistent over the many years of its development. The end result is that, in Guido’s own words, “Even if you are in fact clueless about language design, you can tell that Python is a very simple language.”

The following pages constitute a “quick start” tutorial to Python designed to give you all the information you need to put together basic scripts and to point you toward resources that can take you further.

## Python on Linux

Fedora comes with Python installed by default, as do many other versions of Linux and UNIX—even Mac OS X comes with Python preinstalled. Part of this is due to convenience: Because Python is such a popular scripting language, preinstalling it saves having to install it later if the user wants to run a script. However, in Fedora’s case, part of the reason for preinstallation is that several of the core system programs are written in Python, including yum itself.
