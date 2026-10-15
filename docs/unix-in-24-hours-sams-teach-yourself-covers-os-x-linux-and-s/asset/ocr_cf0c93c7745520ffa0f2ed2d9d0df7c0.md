# Hour 23. Perl Programming in Unix

# Goals for This Hour

In this hour, you will learn

+   - About Exchange, a demonstration currency translator written in Perl
+   - How to check code quality with -w
+   - About online Perl documentation and information
+   - About other useful Perl commands

In this hour, I introduce you to the Perl scripting and programming language. Perl is an interpreted language, so it doesn’t require you to use a compiler as an intermediate step in getting it to work, as C and Java do. Perl works much more like shell scripts, which makes it an easier-to-use development tool.

Whether or not you plan on getting involved with Unix programming, I definitely encourage you to read more about Perl. In addition to being an elegant and powerful Unix tool builder, Perl is also one of the classic programming languages of choice for Web professionals. Want to delve deeper into Web development, though? Then you’d be smart to learn PHP and Python. Both are definitely Unix friendly, and more and more code is being written in those languages, along with Ruby.

In this hour, you’ll learn what tools are available with the standard Perl distribution to help you develop smart, fast programs. This lesson describes a program that enables you to do easy currency translation to prepare for travel overseas.

# Note

Surprisingly, Perl isn’t included with every Unix implementation. If you don’t have it, or if your version of Perl is earlier than 5.0 (try perl -v to find out what version you have), then go to http://www.perl.org to find out about downloading a newer version.

# Flexible and Powerful: Perl

Programming in C, the language developed alongside the Unix operating system, offers considerable flexibility. C is the core language of the Unix operating system itself, but it was originally designed for system-level programming tasks. Perl, by contrast, was designed to be a powerful language for string or word processing. You can most easily see the difference by exploring a programming task, so that’s what we’ll do in this hour of the book.