
## Reference

The first place to look is in the Perl documentation and Linux man pages.

Perl, all of its documentation, and millions of lines of Perl programs are all available free on the Internet. A number of Usenet newsgroups are also devoted to Perl, as well as shelves of books and a quarterly journal.

## Books

Although your local bookstore might have dozens of titles on Perl, the following are some of the more highly recommended of these. You might also look at the *Camel Critiques* (Tom Christiansen; http://language.perl.com/critiques/index.html) for reviews of other available Perl books.

- *Advanced Perl Programming*, by Sriram Srinivasan, O'Reilly & Associates
- *Sams Teach Yourself Perl in 21 Days, Second Edition*, by Laura Lemay, Sams Publishing
- *Sams Teach Yourself Perl in 24 Hours, Second Edition*, by Clinton Pierce, Sams Publishing
- *Learning Perl, Third Edition*, by Randal L. Schwartz, Tom Phoenix, O'Reilly & Associates
- *Programming Perl, Third Edition*, by Larry Wall, Tom Christiansen, and Jon Orwant, O'Reilly & Associates
- *Effective Perl Programming: Writing Better Programs with Perl*, by Joseph Hall, Addison-Wesley Publishing Company
- *CGI Programming with Perl, Second Edition*, by Gunther Birznies, Scott Guelich, Shishir Gundavaram, O'Reilly & Associates
- *Mastering Regular Expressions*, by Jeffrey Friedl, O'Reilly & Associates

## Usenet

Check out the following on Usenet:

- comp.lang.perl.misc—Discusses various aspects of the Perl programming language. Make sure that your questions are Perl specific, not generic CGI programming questions. The regulars tend to flame folks who don't know the difference.
- comp.infosystems.www.authoring.cgi—Discusses authoring of CGI programs, so much of the discussion is Perl specific. Make sure that your questions are related to CGI programming, not just Perl. The regulars are very particular about staying on topic.

## WWW

Check these sites on the World Wide Web:

- http://www.perl.com/—Tom Christiansen maintains the Perl language home page. This is the place to find all sorts of information about Perl, from its history and culture to helpful tips. This is also the place to download the Perl interpreter for your system.
- http://www.perl.com/CPAN/—This is part of the site just mentioned, but it merits its own mention. CPAN (Comprehensive Perl Archive Network) is the place for you to find modules and programs in Perl. If you write something in Perl that you think is particularly useful, you can make it available to the Perl community here.
- http://www.perl.com/pub/q/FAQs—Frequently Asked Questions index of common Perl queries; this site offers a handy way to quickly search for answers about Perl.
- http://learn.perl.org/—One of the best places to start learning Perl online. If you master Perl, go to http://jobs.perl.org.
- http://www.hwg.org/—The HTML Writers Guild is a not-for-profit organization dedicated to assisting web developers. One of its services is a plethora of mailing lists. The hwg-servers mailing list and the hwg-languages mailing list are great places for asking Perl-related questions.
- http://www.pm.org/—The Perl Mongers are local Perl users groups. There might be one in your area. The Perl advocacy site is http://www.perl.org.
- http://www.tpj.com/—*The Perl Journal* is “a reader-supported monthly e-zine” devoted to the Perl programming language. *TPJ* is always full of excellent, amusing, and informative articles, and is an invaluable resource to both new and experienced Perl programmers.
- http://www-106.ibm.com/developerworks/linux/library/l-p101/—A short tutorial about one-line Perl scripts and code.

## Other

Other valuable resources not falling into any of the preceding categories are Perl-related Internet Relay Chat channels. You can usually find several channels available on an IRC server. However, the questions, discussions, and focus of similarly named channels will vary from server to server.

For example, a `#perlhelp` channel is usually for general questions about installing, using, and learning about Perl. A `#perl` channel is generally for more advanced questions, but on some servers beginner questions might be welcomed. You might also find some helpful answers on `#cgi` and `#html` channels. Browse to http://perl-begin.berlios.de/irc/ for a list of servers.

# CHAPTER 30
## Working with Python

As PHP has come to dominate the world of web scripting, Python is increasingly dominating the domain of command-line scripting. Python's precise and clean syntax makes it one of the easiest languages to learn, and it allows programmers to code more quickly and spend less time maintaining their code. Although PHP is fundamentally similar to Java and Perl, Python is closer to C and Modula-3, and so it might look unfamiliar at first.

Most of the other languages have a group of developers at their cores, but Python has Guido van Rossum—creator, father, and Benevolent Dictator For Life (BDFL). Although Guido spends less time working on Python now, he still essentially has the right of veto changes to the language, which has enabled it to remain consistent over the many years of its development. The end result is that, in Guido's own words, “even if you are in fact clueless about language design, you can tell that Python is a very simple language.”

The following pages constitute a “quick start” tutorial to Python designed to give you all the information you need to put together basic scripts and to point you toward resources that can take you further.

### Python on Linux

Fedora comes with Python installed by default, as do many other versions of Linux and Unix—even Mac OS X comes with Python preinstalled. Part of this is due to convenience because it is such a popular scripting language and it saves having to install it later if the user wants to run a script. However, in Fedora's case, part of the reason is that several of the core system programs are written in Python, including Yum itself.

### IN THIS CHAPTER

- Python on Linux
- The Basics of Python
- Functions
- Object Orientation
- The Standard Library and the Vaults of Parnassus
- Reference

If, for some reason, you manage to have a Fedora install without Python, you can install it using Yum using the command `yum install python` as root.

The Python binary is installed into `/usr/bin/python`; if you run that, you will enter the Python interactive interpreter where you can type commands and have them executed immediately. Although PHP also has an interactive mode (use `php -a` to activate it), it is neither as powerful or as flexible as Python's.

As with Perl, PHP, and other scripting languages, you can also execute Python scripts by adding a shebang line to the start of your scripts that point to `/usr/bin/python` and then setting the file to be executable.

The third and final way to run Python scripts is through `mod_python`, which is installed by default when you select the Web Server application group from the Add/Remove Packages dialog.

For the purposes of this introduction, we will be using the interactive Python interpreter because it provides immediate feedback on commands as you type them. Furthermore, knowledge of the interactive interpreter is essential for debugging when you start writing more advanced scripts.

### Getting Interactive

We will be using the interactive interpreter for this chapter, so it is essential that you are comfortable using it. To get started, open a terminal and run the command `python`. You should see this:

```
[paul@caitlin ~]$ python
Python 2.3.4 (#1, Oct 26 2004, 16:42:40)
[GCC 3.4.2 20041017 (Red Hat 3.4.2-6.fc3)] on linux2
Type "help", "copyright", "credits" or "license" for more information.
>>>
```

The `>>>` is where you type your input, and you can set and get a variable like this:

```
>>> python = 'great'
>>> python
'great'
>>>
```

On line one, the variable `python` is set to the text `great`, and on line two that value is read back from the variable simply by typing the name of the variable you want to read. Line three shows Python printing the variable; on line four you are back at the prompt to type more commands.

Python remembers all the variables you use while in the interactive interpreter, which means you can set a variable to be the value of another variable.
