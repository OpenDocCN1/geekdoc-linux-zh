
## HASH VARIABLES

A hash variable, sometimes called an associative array variable, is a plural data structure that holds an array of key-value pairs. It uses strings as keys (indexes) and is optimized to return a value quickly when given a key. Each key must be a unique scalar. Hashes are unordered; arrays (page 1053) are ordered. When you assign a hash to a list, the key-value pairs are preserved, but their order is neither alphabetical nor the order in which they were inserted into the hash; instead, the order is effectively random.

Perl provides two syntaxes to assign values to a hash. The first uses a single assignment statement for each key-value pair:

```perl
$ cat hash1.pl
#!/usr/bin/perl -w
$hashvar1{boat} = "tuna";
$hashvar1{"number five"} = 5;
$hashvar1{4} = "fish";

@arrayhash1 = %hashvar1;
say "@arrayhash1";

$ ./hash1.pl
boat tuna 4 fish number five 5
```

Within an assignment statement, the key is located within braces to the left of the equal sign; the value is on the right side of the equal sign. As illustrated in the preceding example, keys and values can take on either numeric or string values. You do not need to quote string keys unless they contain SPACES. This example also shows that you can display the keys and values held by a hash, each separated from the next by a SPACE, by assigning the hash to an array variable and then printing that variable enclosed within double quotation marks.

The next example shows the other way of assigning values to a hash and illustrates how to use the keys and values functions to extract keys and values from a hash. After assigning values to the %hash2 hash, **hash2.pl** calls the keys function with an argument of %hash2 and assigns the resulting list of keys to the @array_keys array. The program then uses the values function to assign values to the @array_values array.

```perl
$ cat hash2.pl
#!/usr/bin/perl -w

%hash2 = (
    boat => "tuna",
    "number five" => 5,
    4 => "fish",
);

@array_keys = keys(%hash2);
say " Keys: @array_keys";

@array_values = values(%hash2);
say "Values: @array_values";
```

```text
$ ./hash2.pl
Keys: boat 4 number five
Values: tuna fish 5
```

Because Perl automatically quotes a single word that appears to the left of the **=>** operator, you do not need quotation marks around **boat** in the third line of this program. However, removing the quotation marks from around **number five** would generate an error because the string contains a SPACE.

## CONTROL STRUCTURES

Control flow statements alter the order of execution of statements within a Perl program. Starting on page 954, Chapter 27 discusses *bash* control structures in detail and includes flow diagrams. Perl control structures perform the same functions as their *bash* counterparts, although the two languages use different syntaxes. The description of each control structure in this section references the discussion of the same control structure under *bash*.

In this section, the **bold italic** words in the syntax description are the items you supply to cause the structure to have the desired effect; the *nonbold italic* words are the keywords Perl uses to identify the control structure, and [...] represents a block (page 1045) of statements. Many of these structures use *true* (i.e., if *expr* is *false*), to control their execution. See if/unless (next) for an example and explanation of a syntax description.

### if/unless

The if and unless control structures are compound statements that have the following syntax:

```perl
if (*expr*) {...}
unless (*expr*) {...}
```

These structures differ only in the sense of the test they perform. The if structure executes the block of statements if *expr* evaluates to *true*; unless executes the block of statements unless *expr* evaluates to *true* (i.e., if *expr* is *false*).

The *if* appears in nonbold type because it is a keyword; it must appear exactly as shown. The *expr* is an expression; Perl evaluates it and executes the block (page 1045) of statements represented by [...] if the expression evaluates as required by the control structure.

**File test operators** The *expr* in the following example, *-r memo1*, uses the *-r* file test operator to determine if a file named *memo1* exists in the working directory and if the file is readable. Although this operator tests only whether you have read permission for the file, the file must exist for you to have read permission; thus it implicitly tests that the file is present. (Perl uses the same file test operators as *bash*; see Table 27-1 on page 957.) If this expression evaluates to *true*, Perl executes the block of statements (in this case one statement) between the braces. If the expression evaluates to *false*, Perl skips the block of statements. In either case, Perl then exits and returns control to the shell.

```perl
$ cat if1.pl
#!/usr/bin/perl -w
if (-r "memo1") {
    say "The file 'memo1' exists and is readable.";
}
$ ./if1.pl
The file 'memo1' exists and is readable.
```

Following is the same program written using the postfix **if** syntax. Which syntax you use depends on which part of the statement is more important to someone reading the code.

```perl
$ cat if1a.pl
#!/usr/bin/perl -w
say "The file 'memo1' exists and is readable." if (-r "memo1");
```

The next example uses a **print** statement to display a prompt on standard output and uses the statement **$entry = <>;** to read a line from standard input and assign the line to the variable $entry. Reading from standard input, working with other files, and use of the magic file handle `<- >` for reading files specified on the command line are covered on page 1066.

### Comparison operators

Perl uses different operators to compare numbers from those it uses to compare strings. Table 28-2 lists numeric and string comparison operators. In the following example, the expression in the **if** statement uses the **==** numeric comparison operator to compare the value the user entered and the number **28**. This operator performs a numeric comparison, so the user can enter **28**, 28.0, or 00028 and in all cases the result of the comparison will be *true*. Also, because the comparison is numeric, Perl ignores both the whitespace around and the **NEWLINE** following the user's entry. The **-w** option causes Perl to issue a warning if the user enters a nonnumeric value and the program uses that value in an arithmetic expression; without this option Perl silently evaluates the expression as *false*.

```perl
$ cat if2.pl
#!/usr/bin/perl -w
print "Enter 28: ";
$entry = <>;
if ($entry == 28) {        # use == for a numeric comparison
    print "Thank you for entering 28.\n";
}
print "End.\n";
$ ./if2.pl
Enter 28: 28.0
Thank you for entering 28.
End.
```

| | Comparison operators |
|---|---|
| **Numeric operators** | **String operators** | **Value returned based on the relationship between the values preceding and following the operator** |
| `==` | `eq` | True if equal |
| `!=` | `ne` | True if not equal |
| `<` | `lt` | True if less than |
| `>` | `gt` | True if greater than |
| `<=` | `le` | True if less than or equal |
| `>=` | `ge` | True if greater than or equal |
| `cmp` | | `0` if equal, `1` if greater than, `-1` if less than |

The next program is similar to the preceding one, except it tests for equality between two strings. The **chomp** function (page 1067) removes the trailing **NEWLINE** from the user's entry—without this function the strings in the comparison would never match. The **eq** comparison operator compares strings. In this example the result of the string comparison is *true* when the user enters the string *five*. Leading or trailing whitespace will yield a result of *false*, as would the string *5*, although none of these entries would generate a warning because they are legitimate strings.

```perl
$ cat if2a.pl
#!/usr/bin/perl  -w
print "Enter the word 'five' : " ;
$entry = <>;
chomp ($entry);
if ($entry eq "five") {     # use eq for a string comparison
    print "Thank you for entering 'five'.\n";
}
print "End.\n";
$ ./if2a.pl
Enter the word 'five': five
Thank you for entering 'five'.
End.
```

#### if...else

The *if...else* control structure is a compound statement that is similar to the bash *if...then...else* control structure (page 958). It implements a two-way branch using the following syntax:

```perl
if ($expr) {...} else {...}
```

**die** The next program prompts the user for two different numbers and stores those numbers in `$num1` and `$num2`. If the user enters the same number twice, an *if* structure executes a **die** function, which sends its argument to standard error and aborts program execution.
