![](bbox=[0.09, 0.11, 0.17, 0.14])

The third statement initializes the array @list. Although this statement is not required, it is good practice to include it to make the code easier to read. The next statement opens the $fh lexical handle. The trailing pipe symbol (|) in the file-ref (page 1000) portion of this open statement tells Perl to pass the command line preceding the pipe symbol to the shell for execution and to accept standard output from the command when the program reads from the file handle. In this case the command uses grep to filter the /etc/group file (page 472) for lines containing the username held in $user. The die statement displays an error message if Perl cannot open the handle.

```
```text
$ cat groupfind.pl
$user = shift || $ENV{"USER"};
say "User $user belongs to these groups:";
@list = ();
open (my $fh, "grep $user /etc/group |") or die "Error: $!\n";
while ($group = <$fh>) {
  chomp $group;
  $group =~ s/(.*?):.*/$1/;
  push @list, $group;
}
close $fh;
@list = sort @list;
say "@list";
```
```

```
```text
$ perl groupfind.pl
User sam belongs to these groups:
adm admin audio cdr crond dialout dip floppy kvm lpadmin ...
```
```

The while structure in groupfind.pl reads lines from standard output of grep and terminates when grep finishes executing. The name of the group appears first on each line in /etc/group, followed by a colon and other information, including the names of the users who belong to the group. Following is a line from this file:

sam:x:1000:max,zach,helen

The line

$group =~ s/(.*?):.*/$1/;

uses a regular expression and substitution to remove everything except the name of the group from each line. The regular expression .*? would perform a greedy match of zero or more characters followed by a colon; putting a question mark after the asterisk causes the expression to perform a nongreedy match (page 1010). Putting parentheses around the part of the expression that matches the string the program needs to display enables Perl to use the string that the regular expression matches in the replacement string. The final .* matches the rest of the line. Perl replaces the $1 in the replacement string with the string the bracketed portion of the regular expression (the part between the parentheses) matched and assigns this value (the name of the group) to $group.