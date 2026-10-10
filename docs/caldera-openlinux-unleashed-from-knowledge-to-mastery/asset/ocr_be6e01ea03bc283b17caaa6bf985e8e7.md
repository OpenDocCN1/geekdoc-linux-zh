Perl (Practical Extraction and Report Language) was developed in the mid 1980s by Larry Wall, who was already responsible for a number of rather important UNIX utilities. Larry claims that Perl really stands for “Pathologically Eclectic Rubbish Lister”. With the birth of the World Wide Web in the early 1990s, Perl took off as the language of choice for CGI programming. With the recent burst of interest in the Open Source movement, Perl has gotten almost as much press as Linux.

Perl, according to Larry, is all about “making easy things easy, and hard things possible.” So many programming languages make you spend an undue amount of time doing stuff to keep the language happy before you ever get around to making it do what you want it to do. Perl lets you get your work done without worrying about things like memory allocation and variable typing.

Perl contains the best features of C, Basic, and a variety of other programming languages, with a hearty dollop of awk, sed, and shell scripting thrown in. Perl has one advantage over the other UNIX tools—it can process binary files (those without line terminators or that contain binary data). `sed` and `awk` cannot do the job.

In Perl, “there is more than one way to do it.” This is the unofficial motto of Perl, and it comes up so often that it is usually abbreviated as TIMTOWTDI. If you are familiar with some other programming language, chances are you can write functional Perl code.

A version of Perl comes with most Linux distributions, but it is typically several versions out of date. This makes sense when you consider the time required to produce and actually distribute a distribution. As of this writing, the current production version of Perl is 5.005_03 (which is Perl version 5 point 5, patch level 3). Version 5.005_61 is available as a developer release (generally considered experimental). You can determine what version of Perl you have installed by typing `perl -v` at a shell prompt.

This chapter focuses on version 5. Many of the examples shown will fail if you try them with version 4 of Perl. If you are using version 4, you should get one of the newer versions. If you are installing a recent Linux distribution, you should have version 5.

Perl is an interpreted language. The interpreter has been ported to just about every operating system known. For UNIX and UNIX-like (Linux, for example) operating systems, you can just download the code from `http://www.perl.com/` and build it yourself.

# # A Simple Perl Program

To introduce you to the absolute basics of Perl programming, Listing 32.1 illustrates a trivial Perl program.