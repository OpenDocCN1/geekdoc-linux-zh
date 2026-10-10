Because Perl scripts are interpreted, you don’t necessarily have to make them executable in order to run them, or even have the interpreter line at the top. If you prefer, although this method is less conveniently “encapsulated” than the previous method, you can run the script as an argument to `perl` itself. This way you can run the program even if the script is not set executable or does not contain the interpreter line:

```
# perl myscript.pl
```

Some arguments to `perl` can be used in either of these contexts. The `-w` switch, for example, turns on warnings in which the Perl interpreter informs you of improperly written code that can execute but isn’t deterministically correct. You can use the `-w` switch in either of the following ways if you want to ensure that the code you wrote is “proper”:

```
# perl -w myscript.pl
```

or

```
#!/usr/bin/perl -w
```

# ## Variables and Operators

A variable in Perl is either a *scalar* or an *array*, which are two different ways of storing pieces of data. This data can take the form of a number (expressed in any of several different ways), a string of text, or other various types of what are known in Perl as *literals*—pieces of data, such as `3` or `car`, whose meanings are exactly as represented. A *scalar* variable (the most common kind) has a name beginning with the dollar sign ($).

The nice thing about Perl is that you never have to worry about whether a number is an *integer*, a *float*, a *short*, a *long*, or whatever. You also don’t need to treat a string as an array of characters, a pointer to a string in memory, or anything like that. Perl handles all that stuff internally. You don’t even have to convert strings to numbers, or vice versa. Perl will recognize if a string has only numbers in it and allow you to multiply it by a number or apply any mathematical operators to it. Everything from the first nonnumerical character in a string onward is dropped, so `123blah` would be treated by numerical operators as `123`, and `blah` would be treated as zero.

Operators are available to modify these variables. There are the mathematical operators you’d expect: `+`, `-`, `*`, and so on. C-style incrementation operators are available (`++` and `--`), as are space-saving composite mathematical operators (`+=`, `-=`, `*=`, and so on). Extra operators include exponentiation (`**`), modulus (%), and the comparison operators used in conditional classes (`>`, `<`, `>=`, `<=`, `==`, and `!`). Strings can be concatenated with the dot operator (`.`) or repeated any number of times using the string repetition operator (x).

Perl makes use of more operators than you are ever likely to need to know about. Full coverage of these operators could fill an entire book, but Table 20.1 lists the purposes of some of the common operators you’re likely to use when writing scripts for use in FreeBSD.