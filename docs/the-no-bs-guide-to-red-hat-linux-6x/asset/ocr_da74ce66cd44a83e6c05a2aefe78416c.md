# PATTERN MATCHING IN PERL

One mystery remains: What’s this (/^#/) stuff all about? Remember the grep command, back in Chapter 8, “Slicing and Dicing,” and the discussion of regular expressions? If you think about it, the little Perl program in the previous example acts a lot like grep, since it sifts through each line and prints it if a pattern is matched.

In Perl, the forward slashes indicate that a pattern match is to be performed. The regular expression inside the slashes defines the search pattern, and $_ is the variable that the search is performed on. In our case, the ^# inside the slashes means to match only lines that begin with the pound sign.

So if we make the previous example a bit more generic, allowing it to get the search pattern and file name from the command line, it will behave almost exactly like the grep utility:

```
open MYFILE, $ARGV[1] or die "Can't open $ARGV[1]: $!\n";
while (<MYFILE>) {
if (/$ARGV[0]/) { print "MATCH: $_"; }
}
```

# LEARN MORE ABOUT PERL

We’ve barely scratched the surface of what you can do with the Perl language. Try the man perl command to get more information on Perl, read Programming Perl by Larry Wall (O’Reilly & Associates), the inventor of the Perl language, or visit the Perl Institute Web site at http://www.perl.org.

# OTHER LINUX PROGRAMMING LANGUAGES

Shell scripts are fine for many tasks, but if you need to do lots of number crunching, string manipulation, or complicated logic flow, look into one of the other languages briefly mentioned in this section.

# THE C LANGUAGE

C is a general-purpose programming language originally written to help in the development of Unix. Most of the Linux operating system is written in C.