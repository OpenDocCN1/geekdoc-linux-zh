
script, but could be of use in a more heterogeneous environment. Listing 2.16 shows the output on a Solaris system.

## LISTING 2.16 Output of df_check.sh

```
Operating system: SunOS 5.9 Generic_112233-11
-----------------------------
/ : 73%
/var : 79%
```

This script can be used as a template for monitoring other parts of a system because it can be easily extended. If you decide to run it once a day using the cron mechanism (see Section 2.4.2, "The cron Mechanism," later in this chapter for more information), the status of the filesystems, regarding available space, is always available.

## 2.3 PERL SCRIPTS

Perl is short for "Practical Extraction and Reporting Language." It is included with most of the *NIX distributions nowadays. Some of them actually rely on the existence of Perl to tackle administrative tasks. Perl was originally created to provide a means to extract and format information found in larger text or log files in an efficient manner. Regardless of its origins, Perl started to evolve into a full-blown programming language; even object-oriented programming techniques are supported.

One aspect that makes Perl unique is its simplicity; it allows you to build handy tools with unmatched ease. Perl feels different when compared to other scripting or even programming languages. Perl was created in a way that allows you to complete easy tasks in an easy way without preventing you from tackling more complicated jobs with it. The most important saying in Perl is this: if the program does its job, it is a good program. Using Perl requires only rudimentary experience in another programming language. If you worked your way through the shell-scripting example, you should be set. If you are a seasoned programmer and you are anxious to learn Perl, you will find many familiar functions in it.

### 2.3.1 Creating a Perl Script

The following Perl script will output a list of all users and their respective UIDs. Start by creating another subdirectory in your project hierarchy; the one used for the examples is called ulist1. Inside this directory, create the RCS directory and a file named ulist1.pl, according to the following description in Listing 2.17.

## LISTING 2.17 Creating the Structure for the Perl Example

```
erikk@unixhost:~> pwd
/export/home/users/erikk/work
erikk@unixhost:~> mkdir ulist1
erikk@unixhost:~> mkdir ulist1/RCS
erikk@unixhost:~> cd ulist1
erikk@unixhost:~> ls -l
total 2
drwxr-xr-x 2 erikk staff 512 Aug 9 16:56 RCS
erikk@unixhost:~> touch ulist1.pl
erikk@unixhost:~> chmod u+x ulist1.pl
erikk@unixhost:~> ls -l
total 2
drwxr-xr-x 2 erikk staff 512 Aug 9 16:56 RCS
-rwxr--r-- 1 erikk staff 0 Aug 9 16:57 ulist1.pl
erikk@unixhost:~>
```

Up to now, the procedure is the same as in the shell example. However, in this case, you will have to determine the path to the Perl interpreter. To find the exact location of programs in the $PATH, you can use the which command. which perl should return something similar to /usr/bin/perl. The contents shown in Listing 2.18 need to be inserted into the file.

## LISTING 2.18 First Version of the Perl Example

```
#!/usr/bin/perl
# $Id$
#
###################################################
#
#    file:        ulist1.pl
#
#    purpose:     lists all users
#                 and their respective IDs
#
#
#    author:      Erik Keller
#
###################################################
```

```
# Variables

# list passwd first
# open the file
open(MY_PWFILE, "/etc/passwd") or die "$0: couldn’t open file: $!";

# loop through the file and print the records
while(<MY_PWFILE>)
{
    print $_;
}

# close the file
close(MY_PWFILE);

# EOF
```

If you have never seen a Perl program before, the following list contains a short explanation of what is going on.

- open(MY_PWFILE, "/etc/passwd") instructs the program to open the file /etc/passwd and attaches it to the Handle MY_PWFILE. A Handle points to the location in the computer’s memory where the file is stored. The program will use it later to access the file. The continuation of the line, or die "$0: couldn’t open file: $!";, tells the program to stop executing in case of an error and to print out the following information: $0 contains the name of the program and $! the description of the error.

- The instruction <MY_PWFILE> is the living proof of how to make things simple in Perl. It means, “as long as you didn’t reach the end of the file the Handle is pointing to.” So while(<MY_PWFILE>) steps through the file, line by line, until the end of it is reached and executes the commands between the curly braces {}.

- print $_; outputs the current record without changing it. The variable $_ is created automatically and contains the current record.

- close(MY_PWFILE); does exactly what it says—it closes the Handle and the file it points to. Make sure to always close the opened files in the program that used them; relying on the operating system to do so could potentially damage the files or create hard to find error conditions.
