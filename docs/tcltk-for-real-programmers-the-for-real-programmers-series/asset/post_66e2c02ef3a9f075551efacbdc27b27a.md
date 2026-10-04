
## 3.1 Overview of the Basics

### 3.1.1 Syntax

Tcl is a position-based language, not a keyword-based language. There are no reserved strings. The first word of Tcl command line has a defined meaning: it must be a Tcl command, either a built-in command, a procedure name, or (when tels is in interactive mode) an external command.

A complete Tcl command is a list of words. The first word must be a Tcl command name or a subroutine name. The following words may be subcommands, options, or arguments to the command. The command is terminated by a newline or a semicolon.

For example, the word puts at the beginning of a command is a command name, but puts in the second position of a command could be a subcommand or a variable name. The Tcl interpreter keeps separate hash tables for the command names and the variable names, so you can have both a puts and a variable name puts in the same function.

# Example 3.1.1-1

```
puts "This is a command with one argument"
    Valid: This is a complete command.
```

```
x=4
Not valid: x is not a command.
```

```
puts one; puts two;
    Valid: This line has two commands.
```

```
puts one puts
    Not valid: The first command is not terminated, so Tcl
interprets it as a puts command with three arguments.
```

### 3.1.2 Grouping Words

The spaces between words are important. Since Tcl doesn't have a set of keywords, it scans commands by checking for symbols separated by white space.

The spaces in a Tcl command are used to determine which words are commands, subcommands, options, or data. If a data string has multiple words but needs to be treated as a single set of data, the string needs to be grouped with quotes ("") or curly braces ({}).

# Chapter 3. Introduction to the Tcl Language

# Example 3.1.2-1

```
if { $x > 2 } {set greater true}
Valid: If the value of x is greater than 2, then the value of
greater is set to "true."
```

```
if{ $x > 2 } {set greater true}
Invalid: No space between if and test left brace.
```

```
if {$x >2}{ {set greater true}
Invalid: No space between test and body left brace.
```

```
set x a b
Invalid: Too many arguments to set.
```

```
set x "a b"
Valid: The variable x is assigned the value a b.
```

```
set x {a b}
Valid: The variable x is assigned the value a b.
```

Quotes and braces are treated differently by the Tcl interpreter. These differences will be discussed in Chapter 4.

### 3.1.3 Comments

A comment is denoted by putting a pound sign (#) in the position where a
command name could be. It is strongly recommended that this be the first
character on a line, but it could be the first character after a semicolon.

# Example 3.1.3-1

```
# This is a comment
Valid: This is a valid comment.
```

```
puts "test" # Comment after a command.
Valid: But not recommended style.
```

```
puts "test" # this is a syntax error.
Invalid: The puts command was not terminated.
```

## 3.1 Overview of the Basics

### 3.1.4 Data Representation

Tcl does not require that you declare variables before using them. The first time you assign a value to a variable name, it allocates space for the data and adds the variable name to the internal tables.

A variable name is an arbitrarily long sequence of letters, numbers, or punctuation characters. Although any characters (including spaces) can be used in variable names, convention is to follow naming rules similar to those in C and Pascal: start a variable name with a letter, followed by a sequence of alphanumeric characters.

The Tcl Style Guide recommends that you start local variable names with an uppercase letter and global variable names with a lowercase letter. The rationale for this is that items are intended for internal use should require more keystrokes than items intended for external use. This document is available on the SunScript Web site (http://script.sun.com), the Scripts Web site (http://www.sunscript.com/resource/doc/), and on the CD-ROM (docco/style.ps).

A variable is referenced by its name. The value assigned to a variable is accessed by placing a dollar sign ($) in front of the variable name. The value of a Tcl variable will always be accessed as a printable string within your script. Internally, it may be a floating-point value or an integer. That will be discussed in Chapter 12.

# Example 3.1.4-1

```
set x four      Set the value of a variable named x to four.
set pi 3.14      Set the value of a variable named pi to 3.14.
puts "pi is $pi"
                Display the string: "pi is 3.14".
set pi*2 6.28     Set the value of a variable named pi*2 to 6.28.
set "bad variable" "Don't Do This"
                Set the value of a variable named bad variable to Don't
                Do This.
```

# Chapter 3. Introduction to the Tcl Language

Notice that the * symbol in the variable name pi*2 does not multiply. The quotes around pi*2 are not needed because the variable name contains no spaces. However, the variable "bad variable" requires quotes because it contains a space.

### 3.1.5 Command Results

If a command returns multiple arguments, they are returned as a list. If a command returns a single argument, it is returned as a string. If a command returns no arguments, an empty string is returned.

The command that receives the result of another command is called back substitution. The command inside the square brackets is executed first, and its result is substituted into the outer command. This is used to pass the output of one command to another.

# Example 3.1.5-1

```
set x "apple banana"
puts $x
apple banana
```

```
set x {apple banana}
puts $x
apple banana
```

```
set x [apple banana]
puts $x
apple banana
```

## 3.2 Data Types

### 3.2 Data Types

The primitive data type in Tcl is the string. The composite data types are list and associative array. Certain objects such as I/O channels, and sockets are accessed via handles. These will be introduced in the next chapter.

Unlike C++, or Java, Tcl is a typeless language. However, certain commands can define what data is allowed. The expr command, which performs math, will generate an error if you try to perform math on non-numeric strings.

### 3.2.1 Strings

All Tcl data are strings. A string can hold alphanumeric or numeric data. Numeric data can be represented in Tcl as integers, floating-point values (with a decimal point), or in scientific notation.

# Example 3.2.1-1

Legitimate

```
set alpha "abcdef"
Assign the string "abcdef" to variable alpha.
```

```
set validString "this is a valid string"
Assign the string "this is a valid string" to variable validString.
```

```
set number 1.234
Assign the number "1.234" to variable number.
```

```
set scientificNotation 1e2
Assign the number "100" to variable scientificNotation.
```

### 3.2.2 Lists

A list is an ordered set of strings, such as "apple banana". The first element of this list is "apple", the second element is "pear", etc. The order of the elements can be changed with Tcl commands for inserting and deleting list elements, but the Tcl interpreter will never modify the order of list elements as a side effect of another operation.

A list may be arbitrarily long, and list elements may be arbitrarily long.

Any string can be considered as a list. The first word in a string can be considered as the first element in a list.

# Chapter 3. Introduction to the Tcl Language

# Bad Strings

set msg {Bad input: "Bogus". Try again.)}
Assign the string "Bad input: "Bogus". Try again." to variable msg. Note the internal quotes. Quotes within a braced string are treated as ordinary characters.

set msg "Bad input: \"Bogus\", Try again."
Assign the string "Bad input: "Bogus". Try again." to variable msg. Note that the internal quotes are escaped. This will be explained in detail in the next chapter.

set msg "Bad input: "Bogus", Try again.
nThe quotes around Bogus aren't escaped and are treated as quotes. The quote before Bogus closes the string, and the rest of the line causes a syntax error.

set badstring "abcdef"
Has only one quote.

set mismatch {this is not a valid string"
Quote and brace mismatch.

set noquote this is not valid string
The set of words must be grouped to be assigned to a variable.
