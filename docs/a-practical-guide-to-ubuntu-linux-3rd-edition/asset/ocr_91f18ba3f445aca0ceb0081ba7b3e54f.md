Book *Programming Perl*, third edition, by Wall, Christiansen, & Orwant, O’Reilly & Associates (July 2000)

# # HELP

Perl is a forgiving language. As such, it is easy to write Perl code that runs but does not perform as you intended. Perl includes many tools that can help you find coding mistakes. The **\-w** option and the **use warnings** statement can produce helpful diagnostic messages. The **use strict** statement (see the *perldebut* man page) can impose order on a program by requiring, among other things, that you declare variables before you use them. When all else fails, you can use Perl’s built-in debugger to step through a program. See the *perldebut* and *perldebug* man pages for more information.

# ## perldoc

You must install the **perl-doc** package before you can use **perldoc**.

The **perldoc** utility locates and displays local Perl documentation. It is similar to *man* (page 136) but specific to Perl. It works with files that include lines of **pod** (plain old documentation), a clean and simple documentation language. When embedded in a Perl program, **pod** enables you to include documentation for the entire program, not just code-level comments, in a Perl program.

Following is a simple Perl program that includes *pod*. The two lines following **=cut** are the program; the rest is *pod*-format documentation.

```
$ cat pod_ex1.pl
#!/usr/bin/perl

=head1 A Perl Program to Say I<Hi there.>

This simple Perl program includes documentation in B<pod>s format.
The following B<=cut> command tells B<perldoc> that what follows
is not documentation.

=cut
# A Perl program
print "Hi there.\n";

=head1 pod Documentation Resumes with Any pod Command

See the B<perldoc.perl.org/perl|pod.html> page for more information
on B<pod> and B<perldoc.perl.org> for complete Perl documentation.
```

You can use Perl to run the program:

```
$ perl pod_ex1.pl
Hi there.
```