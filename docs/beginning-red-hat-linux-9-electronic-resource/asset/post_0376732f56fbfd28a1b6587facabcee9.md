
```perl
use strict;  # "strict" mode
my (@data);  # Pre-declare array
open (FILE, '/etc/passwd') || die "Cannot open file: $!\n";  # Open the file
while (<FILE>) {  # Read each record
    @data = split (/:/, $_, 7);  # Separate the elements
    print "$data[0], $data[4]\n";  # Print login, comments
}
close (FILE);  # Close file
exit (0);  # Exit application
```

Perl provides us with flexibility to develop applications in the manner that we choose; it imposes very few restrictions upon us. Take, for example, the declaration of variables. By default, we don't have to pre-declare variables before using them in the program. Once you refer to a new variable, it is automatically instantiated and has an undefined value until you provide it with a set value. Unfortunately, this is not good programming practice and should be avoided, since it makes finding errors in your code very difficult if something goes wrong.

Lucky for us, Perl comes with the `strict` pragma, which, when enabled, requires us to pre-declare variables before using them and forces us to avoid symbolic references and bareword identifiers. We will look at the latter two requirements in other examples. But, what exactly is a pragma? A pragma is either an internal module, an outside extension, or a combination of the two that specifies the rules that Perl should follow when processing code.

### Using strict

This brings us to the first line of our application. The `use` function imports functionality from an external module into our current application. We call on this function with the `strict` argument to enable the `strict` pragma. That is all that is needed to force us to pre-declare variables from here on. As a side note, if you look in the Perl extensions directory, typically `/usr/lib/perl5/5.8.0`, you will see a file titled `strict.pm`; this is the file that will be loaded.

Next, we use the `my` function to declare, or localize, the `@data` array. An array is simply a data type, represented by the leading at-sign character, that we can use to store a set of scalar (single) values in one variable. We will use this array to store all of the individual elements for each record in the file, including login and comment.

### Opening the File

We proceed to open the configuration file, `/etc/passwd`, using the `open` function. This function takes two arguments, the first being the file handle that we want to use and the second the path to the file. Think of the handle as a communications channel through which we can read data from the file. If the `open` function executes successfully, which means that the file exists and we have the necessary permissions, it returns a positive (true) status. In Perl, a status of true is represented by a defined non-zero value, and a status of false is identified with an undefined or zero value or a null string.

If we cannot open the file, we call the `die` function with a specific error message to exit from the program. Notice the `$!` expression within the double quoted message string. Expressions that start with the dollar sign represent scalar variables. We can use a scalar variable to store a single value, whether it is a character, number, a text string or even a paragraph of content. However, the `$!` is a special Perl scalar variable that holds the latest error message, returned by either a system function call or a user-defined procedure. Typical failure messages for `open` include 'Permission denied' and 'No such file or directory'.

Look again at the entire line that is trying to open the file, and think of it as two separate statements separated by the logical OR operator, `||`. The second statement will be executed only if the first statement is false; if the file cannot be opened. We are using a convenient shortcut, but you can just as easily rewrite that code as:

```perl
if (!open (FILE, '/etc/passwd')) {
    die "Cannot open file: $!\n";
}
```

The exclamation point in front of the `open` function call will negate the status returned by the function. In other words, it will convert a true value into a false, and vice versa. So, only if the entire expression within the main parentheses is true, will we end up calling the `die` function to terminate our program. And that will happen if the `open` function returns a false status.

We can also write the same statement like this:

```perl
if (open (FILE, '/etc/passwd')) {    # Success
    # Read file
    # Parse records
    # Print output
} else {                               # Failure!
    die "Cannot open file: $!\n";
}
```

This should be easy enough to understand by now; if the `open` function returns true, we process the file or else we exit. Now, we are ready to read data from the file. But, how do we know how many records to read? Simple, we use a `while` loop to iterate through the file, reading one record at a time, until there are no more records to be read. And for each record retrieved from the file, Perl will execute the block of code inside the loop.

### Reading Records

The expression located inside the parenthesis after the `while` command controls when the loop will terminate; the loop will continue until this expression evaluates to a false value. The strange looking expression is the one responsible for reading a line from the *FILE* filehandle and storing it in the default Perl variable, `$_`. When there are no more lines to read, Perl will return an undefined value, or `undef` for short. Once this happens, the expression will evaluate to a false value and the while loop will stop.

Whenever you see such an expression – an identifier of some sort enclosed between a less-than and a greater-than sign – you should know that Perl is reading data from the filehandle represented by that identifier. We can store each record read from the file in a variable other than `$_` by doing the following:

```perl
while ($line = <FILE>) { . . . . . . }
```

Looking inside the loop, we see two statements. These are the ones that are responsible for pulling out the different elements from each record and displaying the login and comment.

### Extracting the Elements

The `split` function separates a piece of text into multiple elements, based on a specified delimiter, and returns an array. It takes three arguments: the delimiter, the input string, and the maximum number of elements. Notice that the delimiter is enclosed within a set of backslash characters; this is an example of a regular expression, or commonly known as **regex**. We can use regular expressions to specify a pattern to match, as opposed to a simple one-character delimiter. We will look at regular expressions in more detail in *Application 3: What is My System Load?*

The last two arguments to the `split` function are optional. If the input string is not specified, Perl uses its default variable, `$_`. This is something you should be aware of. A large number of Perl functions operate on this default variable, so it is very convenient. We have seen two examples of it already: reading records from a filehandle and now the `split` function. The last, but not least, if you don’t specify a maximum number of elements, you won’t see a difference a majority of the time. However, there will be occasions when the last element in the text string is null, in which case, `split` will strip and remove this element. To be on the safe side, you should specify the number of elements that you expect to get back, so there are no surprises!

Once the `split` function returns the elements, we store them in the `@data` array. Each item in an array is associated with a specific position or index, starting at index zero. We can access a specific element in an array by specifying its associated index within brackets. We use the `print` command to display the first and sixth elements to the terminal, followed by a newline.

We repeat this process for all the records in the file. And once the while loop terminates, we close the file using its filehandle and exit from the application. This completes our first major Perl application!
