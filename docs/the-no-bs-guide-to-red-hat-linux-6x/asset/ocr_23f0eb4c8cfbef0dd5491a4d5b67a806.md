Here's a very simple Perl script:

```
#!/usr/bin/perl
print "I am here. \n";
```

The mysterious first line starting with “pound splat slash” is required for all Perl scripts to run; it tells the system where to find the Perl interpreter. Hopefully, you’ve already figured out that this program prints a message followed by the newline character.

Unlike the echo command in Bash scripts, Perl’s print command doesn’t automatically send a carriage return and line feed. If you forget the \n sequence, the next print command will start on the same line. Also note that all Perl statements must end with a semicolon.

# VARIABLES AND QUOTING

A variable in a Perl script is a means of referencing a numeric or character value. As in Bash scripts, Perl doesn’t require you to declare a type for your variables. Perl figures out by context whether the value should be treated as a number or a character string and will even perform character-to-numeric value conversions when necessary. To assign or access the value (contents) of a variable, prefix it with a dollar sign. Spaces before or after the equal sign are optional, but if you want to assign a variable that contains character data, you must put quotation marks around the string.

```
$num=5;
$stuff = "chocolate truffles";
$user = $ENV{USER};
```

In these examples, Perl assigns 5 to the numeric variable $num, “chocolate truffles” to the variable $stuff, and the value of the USER environment variable to $user.

This is a good time to note that there are several distinct ways to use quotation marks in a Perl script. Let’s look at the differences among single quotation marks, double quotation marks, backticks, and the backslash character and then follow up with some examples.

+   - Single quotation marks, as in the preceding example, will always get you exactly what’s inside the quotation marks—any characters that might otherwise have special meaning (like the dollar sign or the backslash) are treated literally.