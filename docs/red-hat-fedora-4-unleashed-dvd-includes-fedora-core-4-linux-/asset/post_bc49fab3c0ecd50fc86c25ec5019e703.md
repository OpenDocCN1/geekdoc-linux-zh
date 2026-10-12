
-I *directory*—Directories specified by -I are prepended to the search path for modules (@INC).

-i[*extension*]—This indicates that files are to be edited in place. If the extension is provided, the original is backed up with that extension. Otherwise, the original file is overwritten.

-l[*octnum*]—Enables automatic line-ending processing, which means that end-of-line characters are automatically removed from input and put back on to output. If the optional octal number is unspecified, this is just the newline character.

-m[*-module*] or -M[*-module*]—Loads the specified module before running your script. There’s a subtle difference between m and M. See perlrun for more details.

-n—Causes Perl to loop around your script for each file provided to the command line. Does not print the output. The following example, from perlrun, deletes all files older than a week:

```
$ find . -mtime +7 -print | perl -nle 'unlink;'
```

-P—This causes your script to be run through the C preprocessor before compilation by Perl.

-p—This is just like -n except that each line is printed.

-S—This searches for the script using the PATH environment variable.

-s—This performs some command-line switch parsing and puts the switch into the corresponding variable in the Perl script. For example, the following script prints '1' if run with the -foobar switch. Your Perl code might look like this:

```
#!/usr/bin/perl -s
print $foobar;
```

When you execute it, you would enter

```
$ ./myperl -foobar
```

-T—This enables taint checking. In this mode, Perl assumes that all user input is tainted, or insecure, until the programmer tells it otherwise. This helps protect you from people trying to exploit security holes in your code and is especially important when writing CGI programs.

-U—This enables you to do unsafe things in your Perl program, such as unlinking directories while running as superuser.

-u—An available, but obsolete switch to tell Perl to dump core after compiling a program.

-V—This prints a summary of the major Perl configuration values and the current value of @INC.

-V: *names*

This parameter displays the value of the names configuration variable.

-v—This prints the version and patch level of your Perl executable. For example,

```
$ perl -v
This is perl, v5.8.4 built for i386-linux-thread-multi
(with 1 registered patch, see perl -V for more detail)
```

Copyright 1987-2003, Larry Wall

Perl may be copied only under the terms of either the Artistic License or the GNU General Public License, which may be found in the Perl 5 source kit.

Complete documentation for Perl, including FAQ lists, should be found on this system using `man perl` or `perldoc perl`. If you have access to the Internet, point your browser at http://www.perl.com/, the Perl Home Page.

-w—This tells Perl to display all warning messages.

-X—This tells Perl to display warning messages about potential problems in the program, such as variables used only once (might be a typo), using = instead of == in a comparison, and the like. This is often used in conjunction with the -c flag to do a thorough program check.

```
$ perl -cw finalassignment.pl
```

-w—This tells Perl to disable all warning messages.

-x directory—This tells Perl that the script is embedded in something larger, such as an email message. Perl throws away everything before a line starting with #!, containing the string 'perl', and everything after _END_. If a directory is specified, Perl changes to the directory before executing the script.

> **NOTE**  
> The Perl documentation is referred to a few times in this section. `perldabug`, `perlrune`, `perlmad`, and `perlmodlib`, for example, are documents from the Perl documentation. To see these documents, just type `perldoc perlmodlib` at the shell prompt. You can also see all the Perl documents online at http://www.cpan.org/doc/index.html or on any CPAN site. CPAN is the Comprehensive Perl Archive Network. See the “Modules and CPAN” section later in this chapter for more information.
> 
> Perl documentation is written in POD (plain old documentation) format and can be converted into any other format, such as TeX, ASCII, or HTML, with the `pod2*` tools that ship with Perl. For example, to produce HTML documentation on the Fubar module, you would type `pod2html Fubar.pm > Fubar.html`.

## Modules and CPAN

A great strength of the Perl community (and the Linux community) is the fact that it is an open-source community. This community support is expressed for Perl via CPAN, which is a network of mirrors of a repository of Perl code.

Most of CPAN is made up of *modules*, which are reusable chunks of code that do useful things, similar to software libraries containing functions for C programmers. These modules help speed development when building Perl programs and free Perl hackers from repeatedly reinventing the wheel when building a bicycle.

There are thousands of Perl modules that do everything from sending email to maintaining your Cisco router access lists to telling you whether a name is masculine or feminine to printing the time in some fancy format. If you can think of doing something with a Perl script, chances are pretty good that a module exists to help you. If there’s no module that helps, you’re encouraged to write one and share it with the rest of the community.

Perl comes with a set of standard modules installed. Those modules should contain much of the functionality that you will initially need with Perl. If you need to use a module not installed with Fedora, use the CPAN module (which is one of the standard modules) to download and install other modules onto your system. At http://www.perl.com/CPAN/, you will find the CPAN Multiplex Dispatcher, which will attempt to direct you to the CPAN site closest to you.

Typing the following command will put you into an interactive shell that gives you access to CPAN. You can type help at the prompt to get more information on how to use the CPAN program.

```
$ perl -MPAN -e shell
```

After you have installed a module from CPAN (or written one of your own), you can load that module into memory where you can use it with the use function:

```
use Time::Ctime;
```

use looks in the directories listed in the variable @INC for the module. In this example, use looks for a directory called Time, which contains a file called Ctime.pm, which in turn is assumed to contain a package called Time::Ctime. The distribution of each module should contain documentation on using that module.

For a list of all the standard Perl modules (those that come with Perl when you install it), see perlmodlib in the Perl documentation. You can read this document by typing perldoc perlmodlib at the command prompt.

## Code Examples

Over the last few years, many people have picked up the notion that Perl is a CGI language, as though it weren’t good for anything else. Nothing could be further from the truth. You can use Perl in every aspect of your system administration and as a building block in whatever applications you’re planning to run on your shiny new Linux system.

The following sections contain a few examples of things you might want to do with Perl.

## Sending Mail

There are several ways to get Perl to send email. One method that you see frequently is opening a pipe to the sendmail command and sending data to it (shown in Listing 29.5). Another method is using the Mail::Sendmail module (available through CPAN or directly at http://www.cpan.org/authors/id/M/MI/MIVKOVIC/), which uses socket connections directly to send mail (as shown in Listing 29.6). The latter method is faster because it does not have to launch an external process. Note that sendmail must be running on your system in order for the Perl program in Listing 29.5 to work.

**LISTING 29.5** Sending Mail Using Sendmail

```
#!/usr/bin/perl
open (MAIL, "| /usr/sbin/sendmail -t"); # Use -t to protect from users
print MAIL <<EndMail;
To: dpitts@mk.net
From: rbowen@mk.net
Subject: Email notification

David,
\tSending email from Perl is easy!
Rich


EndMail
close MAIL;
```

**NOTE**

> Note that the @ sign in the email addresses must be escaped so that Perl does not try to evaluate an array of that name. That is, dpitts@mk.net will cause a problem, so you need to use dpitts\@mk.net.
> 
> The syntax used to print the mail message is called a *here document*. The syntax is as follows:
> 
> print <<EndText;
> ....
> EndText
> 
> The EndText value must be identical at the beginning and at the end of the block, including any whitespace.

**LISTING 29.6** Sending Mail Using the Mail::Sendmail Module

```
#!/usr/bin/perl
use Mail::Sendmail;
%mail = ('To' => 'dpitts@mk.net',
		'From' => 'rbowen@mk.net'
		'Subject' => 'Email notification',
		'Message' => 'Sending email from Perl is easy!',
	);
sendmail(%mail);
```
