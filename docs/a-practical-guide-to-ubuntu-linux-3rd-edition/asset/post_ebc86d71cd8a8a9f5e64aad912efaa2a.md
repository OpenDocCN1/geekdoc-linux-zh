
3. Zero or more occurrences of the preceding character (\*) followed by
4. A closing brace followed by
5. A SPACE.

(A caret as the first character of a character class specifies the class of all characters that do not match the following characters, so [\^\]} matches any character that is not a closing brace.)

```
$ cat re5b.pl
$string = "A line {remove me} may have two {keep me} pairs of braces.";
$string =~ s/([\^\])\*}.*}}/ ;;
print "$string\n";

$ perl re5b.pl
A line may have two {keep me} pairs of braces.
```

Perl provides a shortcut that allows you to specify a nongreedy match. In the following example, the question mark in [.\*?\] causes the regular expression to match the shortest string that starts with an opening brace followed by any string of characters followed by a closing brace.

```
$ cat re5c.pl
$string = "A line {remove me} may have two {keep me} pairs of braces.";
$string =~ s/.[\*?] ;;
print "$string\n";

$ perl re5c.pl
A line may have two {keep me} pairs of braces.
```

# BRACKETING EXPRESSIONS

As explained on page 1094, you can bracket parts of a regular expression and recall those parts in the replacement string. Most Linux utilities use quoted parentheses (i.e., \[ and \]) to bracket a regular expression. In Perl regular expressions, parentheses are special characters. Perl omits the backslashes and uses unquoted parentheses to bracket regular expressions. To specify a parenthesis as a regular character within a regular expression in Perl, you must quote it (page 1093).

The next example uses unquoted parentheses in a regular expression to bracket part of the expression. It then assigns the part of the string that the bracketed expression matched to the variable that held the string in which Perl originally searched for the regular expression.

First the program assigns the string *My name is Sam* to $stg. The next statement looks for a match for the regular expression /.*My name is .*/ in the string held by $stg. The part of the regular expression bracketed by parentheses matches *Sam*; the $1 in the replacement string matches the first (and only in this case) matched bracketed portion of the regular expression. The result is that the string held in $stg is replaced by the string *Sam*.

```
$ cat re11.pl
$stg = "My name is Sam";
$stg =~ s/My name is (.*)/$1/;
print "Matched: $stg\n";

$ perl re11.pl
Matched: Sam
```

The next example uses regular expressions to parse a string for numbers. Two variables are initialized to hold a string that contains two numbers. The third line of the program uses a regular expression to isolate the first number in the string. The \D matches a string of zero or more characters that do not include a digit: The \D special character matches any single nondigit character. The trailing asterisk makes this part of the regular expression perform a greedy match that does not include a digit (it matches **What** is ). The bracketed regular expression \d+ matches a string of one or more digits. The parentheses do not affect what the regular expression matches; they allow the $1 in the replacement string to match what the bracketed regular expression matched. The final .* matches the rest of the string. This line assigns the value of the first number in the string to $string.

The next line is similar but assigns the second number in the string to $string2. The print statements display the numbers and the result of subtracting the second number from the first.

```
$ cat re8.pl
$string = "What is 488 minus 78?";
$string2 = $string;
$string =~ s/\D+(\d+).*\$1/;
$string2 =~ s/\D+(\d+)\D+(\d+).*\$1/;

print "$string\n";
print "$string2\n";
print $string - $string2, "\n";

$ perl re8.pl
488
78
410
```

The next few programs show some of the pitfalls of using unquoted parentheses in regular expressions when you do not intend to bracket part of the regular expression. The first of these programs attempts to match parentheses in a string with unquoted parentheses in a regular expression, but fails. The regular expression ag( ed) matches the same string as the regular expression ag because the parenthesis is a special character; the regular expression does not match the string ag(ed).

```
$ perl -le 'if ("ag(ed)") {print "true";} else {print "false";}'
false
```

The regular expression in the next example quotes the parentheses by preceding each with a backslash, causing Perl to interpret them as regular characters. The match is successful.

```
$ perl -le 'if ("ag(ed)" =~ /ag\(ed\)/) {print "true";} else {print "false";}'
true
```

Next, Perl finds an unmatched parenthesis in a regular expression:

```
$ perl -le 'if ("ag(ee" =~ /ag(e/) {print "true";} else {print "false";}'
Unmatched ( in regex; marked by <-- HERE in m/ag/( <-- HERE e/ at -e line 1.
```

When you quote the parenthesis, all is well and Perl finds a match:

```
$ perl -le 'if ("ag(ed)" =~ /ag\(ed\)/) {print "true";} else {print "false";}'
true
```

# CPAN MODULES

CPAN (Comprehensive Perl Archive Network) provides Perl documentation, FAQs, modules (page 1045), and scripts on its Web site (www.cpan.org). It holds more than 16,000 distributions (page 1045) and provides links, mailing lists, and versions of Perl compiled to run under various operating systems (ports of Perl). One way to locate a module is to visit search.cpan.org and use the search box or click one of the classes of modules listed on that page.

This section explains how to download a module from CPAN and how to install and run the module. Perl provides a hierarchical namespace for modules, separating components of a name with double colons (::). The example in this section uses the module named **Timestamp::Simple**, which you can read about and download from search.cpan.org/dist/Timestamp-Simple. The timestamp is the date and time in the format **YYYYMMDDHHMMSS**

To use a Perl module, you first download the file that holds the module. For this example, the search.cpan.org/~shoop/Timestamp-Simple-1.01/Simple.pm Web page has a link on the right side labeled **Download**. Click this link and save the file to the directory you want to work in. You do not need to work as a privileged user until the last step of this procedure, when you install the module.

Most Perl modules come as compressed **tar files** (page 176). With the downloaded file in the working directory, decompress the file:

```
$ tar xzvf Timestamp-Simple-1.01.tar.gz
Timestamp-Simple-1.01/
Timestamp-Simple-1.01/Simple.pm
Timestamp-Simple-1.01/Makefile.PL
Timestamp-Simple-1.01/README
Timestamp-Simple-1.01/test.pl
Timestamp-Simple-1.01/Changes
Timestamp-Simple-1.01/MANIFEST
Timestamp-Simple-1.01/ARTISTIC
Timestamp-Simple-1.01/GPL
Timestamp-Simple-1.01/META.yml
```

The **README** file in the newly created directory usually provides instructions for building and installing the module. Most modules follow the same steps.

```
$ cd Timestamp-Simple-1.01
$ perl Makefile.PL
Checking if your kit is complete...
Looks good
Writing Makefile for Timestamp::Simple
```

If the module you are building depends on other modules that are not installed on the local system, running `perl Makefile.PL` will display one or more warnings about prerequisites that are not found. This step writes out the makefile even if modules are missing. In this case the next step will fail, and you must build and install missing modules before continuing.

The next step is to run **make** on the makefile you just created. After you run **make**, run **make test** to be sure the module is working.

```
$ make
cp Simple.pm blib/lib/Timestamp/Simple.pm
Manifying blib/man3/Timestamp::Simple.3pm
```

```
$ make test
PERL_DL_NONLAZY=1 /usr/bin/perl "-Iblib/lib" "-Iblib/arch" test.pl
1..1
# Running under perl version 5.10.0000 for linux
# Current time local: Fri Sep 3 18:20:41 2010
# Current time GMT: Sat Sep 4 01:20:41 2010
# Using Test.pm version 1.25
ok 1
ok 2
ok 3
```

Finally, running with root privileges, install the module:

```
$ sudo make install
Installing /usr/local/share/perl/5.10.0/Timestamp/Simple.pm
Installing /usr/local/man/man3/Timestamp::Simple.3pm
Writing /usr/local/lib/perl/5.10.0/auto/Timestamp/Simple/.packlist
Appending installation info to /usr/local/lib/perl/5.10.0/perllocal.pod
```

Once you have installed a module, you can use **perldoc** to display the documentation that tells you how to use the module. See page 1043 for an example.

Some modules contain **SYNOPSIS** sections. If the module you installed includes such a section, you can test the module by putting the code from the **SYNOPSIS** section in a file and running it as a Perl program:

```
$ cat times.pl
use Timestamp::Simple qw{stamp};
print stamp, "\n";

$ perl times.pl
20100904182627
```
