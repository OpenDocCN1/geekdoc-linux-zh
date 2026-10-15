
## Get names with get_string and convert to uppercase
```sh
$fname = get_string "First name";
$lname = uc get_string "Last name";
printf "Whole name: $fname $lname\n";
```

The output:
```
$ perl validate
First name: John Ball
Last name: Park
Whole name: JOHN BALL PARK
```

The get_string function and the for loop both illustrate the use of the my operator to create variables of local scope. By default, all variables are global in Perl.

The list of local variables for get_string is initialized with a single scalar drawn from the routine’s argument array. Variables in the initialization list that have no corresponding value (here, $response) remain undefined.

The *STDIN passed to the readline function is a “typeglob,” a festering wart of language design. It’s best not to inquire too deeply into what it really means, lest one’s head explode. The short explanation is that Perl filehandles are not first-class data types, so you must generally put a star in front of their names to pass them as arguments to functions.

In the assignments for $fname and $lname, the uc (convert to uppercase) and get_string functions are both called without parentheses. Since there is no possibility of ambiguity given the single argument, this works fine.

## Perl as a filter

You can use Perl without a script by putting isolated expressions on the command line. This is a great way to do quick text transformations and one that largely obsoletes older filter programs such as **sed**, **awk**, and **tr**.

Use the **-pe** command-line option to loop through STDIN, run a simple expression on each line, and print the result. For example, the command

```sh
ubuntu$ perl -pe 's#/bin/sh$#/bin/bash#' /etc/passwd
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/bin/bash
...
```

replaces **/bin/sh** at the end of lines in **/etc/passwd** with **/bin/bash**, emitting the transformed **passwd** file to STDOUT. You may be more accustomed to seeing the text substitution operator with slashes as delimiters (e.g., **s/foo/bar/**), but Perl allows any character. Here, the search text and replacement text both contain slashes, so it’s simpler to use # as the delimiter. If you use paired delimiters, you must use four of them instead of the normal three, e.g., **s(foo)(bar)**.

Perl's -a option turns on autosplit mode, which separates input lines into fields that are stored in the array named @F. Whitespace is the default field separator, but you can set another separator pattern with the -F option.

Autosplit is handy to use in conjunction with -p or its nonauto printing variant, -n. For example, the commands below use perl -ane to slice and dice the output from two variations of df. The third line then runs join to combine the two sets of fields on the Filesystem field, producing a composite table that includes fields drawn from both versions of the df output.

```
suse$ df -h | perl -ane 'print join("	", @F[0..4]), "\n"' > tmp1
suse$ df -i | perl -ane 'print join("	", @F[0,1,4]), "\n"' > tmp2
suse$ join tmp1 tmp2
```

| Filesystem | Size | Used | Avail | Use% | Inodes | IUse% |
|---|---|---|---|---|---|---|
| /dev/hda3 | 3.0G | 1.9G | 931M | 68% | 393216 | 27% |
| udev | 126M | 172K | 126M | 1% | 32086 | 2% |
| /dev/hda1 | 92M | 26M | 61M | 30% | 24096 | 1% |
| /dev/hda6 | 479M | 8.1M | 446M | 2% | 126976 | 1% |
| ... |  |  |  |  |  |  |

A script version with no temporary files would look something like this:

```
#!/usr/bin/perl

for (split(/\n/, `df -h`)) {
  @F = split;
  $h_part{$F[0]} = [ @F[0..4] ];
}

for (split(/\n/, `df -i`) {
  @F = split;
  print join("\t", @{$h_part{$F[0]}}, $F[1], $F[4]), "\n";
}
```

The truly intrepid can use -i in conjunction with -pe to edit files in place; Perl reads the files in, presents their lines for editing, and saves the results out to the original files. You can supply a pattern to -i that tells Perl how to back up the original version of each file. For example, -i.bak backs up passwd as passwd.bak. Beware—if you don't supply a backup pattern, you don't get backups at all. Note that there's no space between the -i and the suffix.

## Add-on modules for Perl

CPAN, the Comprehensive Perl Archive Network at cpan.org, is the warehouse for user-contributed Perl libraries. Installation of new modules is greatly facilitated by the cpan command, which acts much like a yum or APT package manager dedicated to Perl modules. If you're on a Linux system, check to see if your distribution packages the module you're looking for as a standard feature—it's much easier to install the system-level package once and then let the system take care of updating itself over time.
