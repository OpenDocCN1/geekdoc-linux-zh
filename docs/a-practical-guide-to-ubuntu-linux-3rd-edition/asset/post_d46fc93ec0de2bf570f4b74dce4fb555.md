
You can then incorporate the module in a Perl program. The following example uses the timestamp module to generate a unique filename:

```perl
$ cat fn.pl
use Timestamp::Simple qw(stamp);

# Save timestamp in a variable
$ts = stamp, "\n";

# Strip off the year
$ts =~ s/...(.*)/^1/;

# Create a unique filename
$fn = "myFile." . $ts;

# Open, write to, and close the file
open (OUTFILE, ">", "$fn");
print OUTFILE "Hi there.\n";
close (OUTFILE);

$ perl fn.pl
$ ls myf*
myFile.0905183010
```

**substr**  
You can use the `substr` function in place of the regular expression to strip off the year. To do so, replace the line that starts with `$ts =~` with the following line. Here, `substr` takes on the value of the string `$ts` starting at position 4 and continuing to the end of the string:

```perl
$ts = substr ($ts, 4);
```

## EXAMPLES

This section provides some sample Perl programs. First try running these programs as is, and then modify them to learn more about programming with Perl.

The first example runs under Linux and displays the list of groups that the user given as an argument is a member of. Without an argument, it displays the list of groups that the user running the program is a member of. In a Perl program, the `%ENV` hash holds the environment variables from the shell that called Perl. The keys in this hash are the names of environment variables; the values in this hash are the values of the corresponding variables. The first line of the program assigns a username to `$user`. The `shift` function (page 1055) takes on the value of the first command-line argument and shifts the rest of the arguments, if any remain. If the user runs the program with an argument, that argument is assigned to `$user`. If no argument appears on the command line, `shift` fails and Perl executes the statement following the Boolean OR (`||`). This statement extracts the value associated with the `USER` key in `%ENV`, which is the name of the user running the program.

Accepting output from a process  
The third statement initializes the array **@list**. Although this statement is not required, it is good practice to include it to make the code easier to read. The next statement opens the **$fh** lexical handle. The trailing pipe symbol (`|`) in the *file-ref* (page 1066) portion of this **open** statement tells Perl to pass the command line preceding the pipe symbol to the shell for execution and to accept standard output from the command when the program reads from the file handle. In this case the command uses **grep** to filter the */etc/group* file (page 492) for lines containing the username held in **$user**. The **die** statement displays an error message if Perl cannot open the handle.

```perl
$ cat groupfind.pl
$user = shift || $ENV{'USER'};
say "User $user belongs to these groups:";
@list = ();
open (my $fh, "grep $user /etc/group |") or die "Error: $!\n";
while ($group = <$fh>) {
  chomp $group;
  $group =~ s/(.*)::.*/$1/;
  push @list, $group;
}
close $fh;
@list = sort @list;
say "@list";
```

```bash
$ perl groupfind.pl
User sam belongs to these groups:
adm admin audio cdrom dialout dip floppy kvm lpadmin ...
```

The **while** structure in **groupfind.pl** reads lines from standard output of **grep** and terminates when **grep** finishes executing. The name of the group appears first on each line in */etc/group*, followed by a colon and other information, including the names of the users who belong to the group. Following is a line from this file:

```plaintext
tom:x:1000:max,zach,helen
```

The line

```perl
$group =~ s/(.*)::.*/$1/;
```

uses a regular expression and substitution to remove everything except the name of the group from each line. The regular expression `.*:` would perform a greedy match of zero or more characters followed by a colon; putting a question mark after the asterisk causes the expression to perform a nongreedy match (page 1076). Putting parentheses around the part of the expression that matches the string the program needs to display enables Perl to use the string that the regular expression matches in the replacement string. The final `.*` matches the rest of the line. Perl replaces the `$1` in the replacement string with the string the bracketed portion of the regular expression (the part between the parentheses) matched and assigns this value (the name of the group) to `$group`.

The **chomp** statement removes the trailing *NEWLINE* (the regular expression did not match this character). The **push** statement adds the value of $fgroup to the end of the @list array. Without **chomp**, each group would appear on a line by itself in the output. After the **while** structure finishes processing input from grep, **sort** orders @list and assigns the result to @list. The final statement displays the sorted list of groups the user belongs to.

### opendir and readdir

The next example introduces the **opendir** and **readdir** functions. The **opendir** function opens a directory in a manner similar to the way **open** opens an ordinary file. It takes two arguments: the name of the directory handle and the name of the directory to open. The **readdir** function reads the name of a file from an open directory.

In the example, **opendir** opens the working directory (specified by .) using the $dir lexical directory handle. If **opendir** fails, Perl executes the statement following the **or** operator: **die** sends an error message to standard error and terminates the program. With the directory opened, **while** loops through the files in the directory, assigning the filename that **readdir** returns to the lexical variable $entry. An **if** statement executes **print** only for those files that are directories (-d). The **print** function displays the name of the directory unless the directory is named . or ... When **readdir** has read all files in the working directory, it returns *false* and control passes to the statement following the **while** block. The **closedir** function closes the open directory and **print** displays a *NEWLINE* following the list of directories the program displays.

```perl
$ cat dirs2a.pl
#!/usr/bin/perl
print "The working directory contains these directories:\n";

dir = my $dir = '.' or die "Could not open directory: $!\n";
while (my $entry = readdir $dir) {
    if (-d $entry) {
        print $entry, ' ' unless ($entry eq '.' || $entry eq '..');
    }
}
closedir $dir;
print "\n";

$ ./dirs2a.pl
The working directory contains these directories:
two one
```

### split

The **split** function divides a string into substrings as specified by a delimiter. The syntax of a call to **split** is

```perl
*split* (*re/, string*);
```

where *re* is the delimiter, which is a regular expression (frequently a single regular character), and *string* is the string that is to be divided. As the next example shows, you can assign the list that **split** returns to an array variable.

The next program runs under Linux and lists the usernames of users with UIDs greater than or equal to 100 listed in the `/etc/passwd` (page 494) file. It uses a **while** structure to read lines from `passwd` into `$user`, and it uses `split` to break the line into substrings separated by colons. The line that begins with `@row` assigns each of these substrings to an element of the `@row` array. The expression the **if** statement evaluates is `true` if the third substring (the UID) is greater than or equal to 100. This expression uses the `>=` numeric comparison operator because it compares two numbers; an alphabetic comparison would use the `ge` string comparison operator.

The **print** statement sends the UID number and the associated username to the `$sortout` file handle. The **open** statement for this handle establishes a pipe that sends its output to `sort -n`. Because the sort utility (page 168) does not display any output until it finishes receiving all of the input, `split3.pl` does not display anything until it closes the `$sortout` handle, which it does when it finishes reading the `passwd` file.

```perl
$ cat split3.pl
#!/usr/bin/perl -w
open ($pass, "/etc/passwd");
open ($sortout, "| sort -n");
while ($user = <$pass>) {
    @row = split (/:/, $user);
    if ($row[2] >= 100) {
        print $sortout "$row[2] $row[0]\n";
    }
}
close ($pass);
close ($sortout);
$ ./split3.pl
100 libuuid
101 syslog
102 klog
103 avahi-autoipd
104 pulse
...
```

The next example counts and displays the arguments it was called with, using `@ARGV` (page 1068). A **foreach** structure loops through the elements of the `@ARGV` array, which holds the command-line arguments. The `++` preincrement operator increments `$count` before it is displayed.

```perl
$ cat 10.pl
#!/usr/bin/perl -w
$count = 0;
$#num = @ARGV;
print "You entered $num arguments on the command line:\n";
foreach $arg (@ARGV) {
    print ++$count, ". $arg\n";
}
```
