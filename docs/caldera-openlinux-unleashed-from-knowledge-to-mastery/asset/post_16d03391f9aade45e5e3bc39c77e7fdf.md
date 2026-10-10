
if ($name eq "Rich") {
 print "Hello, Rich!\n";
}

Alternatively, you can write it as you would more likely say it:

print "Hello Rich!\n" if $name eq "Rich";

Larry designed Perl as a natural language. In this respect, it is different from most other programming languages. The traditional computer science way of doing things is to have a minimal set of keywords from which all other concepts are built. Perl, on the other hand, provides you with more than one way to say the same thing (TIMTOWTDI) like a spoken language would.

Also like spoken language, Perl evolved as it was used. If people saw a need for a particular function or a new syntax, Larry included it in the next version. If nobody used a particular feature, or everyone hated a particular construct, Larry threw it out. As Larry put it, "I picked the feature set of Perl because I thought they were cool features. I left the other ones behind because I thought they sucked."

## unless

unless works just like if, only backward. unless performs a statement or block if a condition is false.

unless ($name eq "Rich")   {
 print "Go away, you're not allowed in here!\n";
}

> **Note**
> You can restate the preceding example in more natural language, as you did in the *if* example.

print "Go away!\n" unless $name eq "Rich";

Although it is not a rule, you should try to put the more important part of the statement (think of it as a sentence) on the left, so that it is easier to read.

## Looping

A *loop* is a way to do something multiple times. A very simple example is a countdown timer that performs a task (waiting for 1 second) 300 times before telling you that your egg is done boiling.

Looping constructs can either perform a block of code as long as certain conditions apply, or while they step through a list of values, perhaps using that list as arguments.

Perl has four looping constructs: for, foreach, while, and until.

## for

The for construct performs a *statement* (block of code) for a set of conditions defined as follows:

for (start condition; end condition; increment function) {
    statement(s)
}

The start condition is set at the beginning of the loop. Each time the loop is executed, the increment function is performed until the end condition is achieved. This looks much like the traditional for/next loop. The following code is an example of a for loop:

for ($i=1; $i<=10; $i++) {
    print "$i\n"
}

## foreach

The foreach construct performs a statement block for each element in a list or array:

foreach $name (@names) {
    print "$name\n"
}

The loop variable ($name in the example) is not merely set to the value of the array elements; it is aliased to that element. This means that if you modify the loop variable, you are actually modifying the array.

If no loop array is specified, as in the following example, the Perl default variable $_ is used:

for (@names)         {
    print "$_ was here!\n";
}

This syntax can be very convenient, but it can also lead to unreadable code. Give a thought to the poor person who will be maintaining your code. It will probably be you.

> **Note**
> *foreach is frequently abbreviated as for.*

## while

while performs a block of statements as long as a particular condition is true:

while ($x<10) {
    print "$x\n";
    $x++;
}

Remember that the condition can be anything that returns a true or false value. For example, it could be a function call:

while (InvalidPassword($user, $password)) {
    print 'You've entered an invalid password. Please try again.\n';
    $password = GetPassword;
}

## until

until is the exact opposite of the while statement. It performs a block of statements as long as a particular condition is false—or, rather, until it becomes true:

until (ValidPassword($user, $password)) {
    print 'You've entered an invalid password. Please try again.\n';
    $password = GetPassword;
}

## last and next

You can force Perl to end a loop early by using the `last` statement. `last` is similar to the C `break` command—the loop is exited. If you decide you need to skip the remaining contents of a loop without ending the loop itself, you can use `next`, which is similar to the C `continue` command. Unfortunately, these do not work with do...while loops.

## do...while and do...until

The while and until loops evaluate the conditional first. This behavior can be changed by applying a do block before the conditional. With the do block, the condition is evaluated last, which results in the contents of the block always executing at least once (even if the condition is false). This is similar to the C language do...while (*conditional*) statement.

## Regular Expressions

Perl's greatest strength is in text and file manipulation, which are accomplished by using the regular expression (regex) library. Regexes allow complicated pattern matching and replacement to be done efficiently and easily.

For example, the following line of code replaces every occurrence of the string bob or the string mary with fred in a line of text:

$string =~ s/bob|mary/fred/gi;

Without going into too many of the details, Table 32.7 explains what the preceding line says.

| Element | Explanation |
| :--- | :--- |
| `$string =~` | Performs this pattern match on the text found in the variable called $string. |
| `s` | Substitute. |
| `/` | Begins the text to be matched. |
| `bob\|mary` | Matches the text bob or mary. You should remember that it is looking for the text mary, not the word mary; that is, it will also match the text mary in the word maryland. |
| `/` | Ends text to be matched; begins text to replace it. |
| `fred` | Replaces anything that was matched with the text fred. |
| `/` | Ends text to be replaced. |
| `g` | Does this substitution globally; that is, replaces the match text wherever in the string you match it (and any number of times). |
| `i` | The search text is case-insensitive. It matches Bob, bOb, or bOB. |
| `;` | Indicates the end of the line of code. |

If you are interested in the details, you can get more information using the regex (5) section of the manual.

Although replacing one string with another might seem a rather trivial task, the code required to do the same thing in another language (for example, C) is rather daunting.

## Access to the Shell

Perl is useful for administrative functions because it has access to the shell. This means Perl can perform any process you might ordinarily perform by typing commands to the shell. You do this with the `\`\` syntax. For example, the following code in Listing 32.4 prints a directory listing.

### LISTING 32.4 Using Backticks to Access the Shell

$curr_dir = `pwd`;
@listing = `ls -la`;
print "Listing for $curr_dir\n";
foreach $file (@listing) {
    print "$file";
}

> **Note**
> The `\` \` notation uses the backtick found above the Tab key (on most keyboards), not the single quotation mark.

You can also use the `Shell` module to access the shell. `Shell` is one of the standard modules that comes with Perl. It gives an even more transparent access to the shell. Look at the following code for an example:

use Shell qw(cp);
cp ('/home/httpd/logs/access.log', "/tmp/httpd.log");

It almost looks as though it is importing the command-line functions directly into Perl. Although that is not really happening, you can pretend that it is and use it accordingly.

A third method of accessing the shell is via the `system` function call:

$rc = 0xfff & system('cp /home/httpd/logs/access.log /tmp/httpd.log');
if ($rc == 0) {
    print "system cp succeeded \n";
}
else {
    print "system cp failed $rc";
}

The `system` function can also be used with the `or` `die` clause:

system('cp /home/httpd/logs/access.log /tmp/httpd.log') == 0
    or die "system cp failed: $?"

However, you cannot capture the output of a command executed through the `system` function.

Access to the command line is fairly common in shell scripting languages, but is less common in higher-level programming languages.
