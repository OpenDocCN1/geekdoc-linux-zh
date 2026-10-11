
## EXPLANATION
- 1 The quoted string is printed to the screen, STDOUT, by default.
- 2 The scalar variable is assigned a single line of text typed in by the user. The `<=>` operator is used for read operations. In this case, it reads from STDIN, which is your keyboard, until the Enter key is pressed. The newline is included in the text that is assigned to the variable $name.
- 3 The value of $name is printed. Note that the newline breaks the line after Joe Smith, the user’s input.
- 4 The `chop` function removes the last character of the string assigned to $name. The character that was chopped is returned.
- 5 The string is printed again after the `chop` operation. The last character was removed (in this `case`, the newline).
- 6 This time `chop` will remove the last character in Joe Smith’s name, which is the `h` in `Smith`.
- 7 The quoted string is printed to STDOUT, indicating that the last character was removed.
- 9 The user input is first assigned to the variable $age. The trailing newline is chopped. The character whose value is stored in the special variable, $\/, is removed. This value is, by default, the newline character. The number of characters chopped is returned. Because of the low precedence of the equal (=) operator, parentheses ensure that the assignment occurs before the `chomp` function chomps.
- 10 The second `chomp` will have no effect. The newline has already been removed, and `chomp` removes only the newline. It’s safer than using `chop`.
- 11 The chopped variable `string` is printed.

### 10.2.3 The read Function

The `read` function¹ allows you to read a number of characters into a variable from a specified filehandle. (The first character is character 0.) If reading from standard input, the filehandle is STDIN. The `read` function returns the number of bytes that were read. You will normally use this function with files or reading input from a server using CGI. To read the entire file you will need to know the size in bytes of that file.

1. The `read` function is similar to the `fread` function in the C language.

### FORMAT

```
number_of_bytes = read(FILEHANDLE, buffer, how_many_bytes);
```

### EXAMPLE 10.13

(The Script)

```perl
use warnings;
# Reading input in a requested number of bytes
print "Describe your favorite food in 10 bytes or less.\n";
print "If you type less than 10 characters, press CTRL+D on a line by itself.\n";
my $number=read(STDIN, $favorite, 10);
print "You just typed: $favorite\n";
print "The number of bytes read was $number.\n";
```

(Output)

```
Describe your favorite food in 10 bytes or less.
If you type less than 10 characters, press CTRL+D on a line by itself.
apple pie and ice cream <user input>
You just typed: apple pie
The number of bytes read was 10.
```

### EXPLANATION

- The user is asked for input. If he types less than 10 characters, he should press <CTRL+D> to exit.
- The read function takes three arguments: the first argument is STDIN, the place from where the input is coming; the second argument is the scalar $favorite, where the input will be stored; and the third argument is the number of characters (bytes) that will be read.
- The 10 characters read in are printed. The rest of the characters were left in the buffer and ignored.
- The number of characters (bytes) actually read was stored in $number and is finally printed.

### 10.2.4 The getc Function

The getc function gets a single character from the keyboard or from a file. At EOF, getc returns a null string.

### SYNTAX

```
getc(FILEHANDLE)
getc FILEHANDLE
getc
```

### EXAMPLE 10.14

(The Script)

```perl
use warnings;
# Getting only one character of input
print "Answer y or n ";

my $answer=gets; # Gets one character from stdin
$restofit=<>; # What remains in the input buffer is # assigned to $restofit

print "$answer\n";
print "The characters left in the input buffer were:
$restofit\n";
```

(Output)

```
Answer y or n y
The characters left in the input buffer were: essirreebob
```

### EXPLANATION

- 1. Only one character is read from the input buffer by getc and stored in the scalar $answer.
- 2. The characters remaining in the input buffer are stored in $restofit. This clears the input buffer. Now, if you ask for input later in the program, you will not be picking up those characters that were left hanging around in the buffer.
- 3. The character that was read in by getc is printed.
- 4. The characters stored in $restofit are displayed.

### 10.2.5 Assigning Input to an Array

When reading input from the filehandle STDIN, if the context is an array, then each line is read with its newline and is treated as a single list item, and the read is continued until you press <CTRL>+D (in UNIX) or <CTRL>+Z (in Windows) at end of file (EOF). Normally, you will not assign input to an array, because it could eat up a large amount of memory, or because the user of your program may not realize that he should press <CTRL>+D or <CTRL>+Z to stop reading input.

(The Script)

```perl
use warnings;
# Assigning input to an array
print "Tell me everything about yourself.\n";
my @all = <STDIN>;
print "all";
print "The number of elements in the array are: ",
      $all + 1, "\n";
print "The first element of the array is: $all[0]";
```

(Output)

- 1 Tell me everything about yourself.
- 2 OK. Let’s see I was born before computers.
- I grew up in the 50s.
- I was in the hippie generation.
- I’m starting to get bored with talking about myself.
- <CTRL>+D
- 3 OK. Let’s see I was born before computers.
- I grew up in the 50s.
- I was in the hippie generation.
- I’m starting to get bored with talking about myself.
- 4 The number of elements in the array are: 4.
- 5 The first element of the array is:
- OK. Let’s see I was born before computers.

### EXPLANATION

- 1 The string Tell me everything about yourself. is printed to STDOUT.
- 2 The input operator <> surrounding STDIN reads input lines until <CTRL>+D. EOF, is reached. (For Windows, use <CTRL>+Z instead of <CTRL>+D.) Each line and its trailing newline are stored as a list element of the array @all.
- 3 The user input is printed to the screen after the user presses <CTRL>+D or <CTRL>+Z.
- 4 The $# construct lets you get the last subscript or index value in the array. By adding 1 to $#all, the size of the array is obtained; that is, the number of lines that were read.
- 5 $all[0] is the first element of the array that evaluates to the first line of input from the user. Each line read is an element of the array.

### 10.2.6 Assigning Input to a Hash

Reading input from STDIN and assigning it to a hash is like reading from a file. The line read can be assigned as a value corresponding to a hash key or as the key itself.

### EXAMPLE 10.16

(The Script)

```perl
use warnings;
# Assign input to a hash
my %course = (); # Empty hash
my $course_number = 101;
print "What is the name of course $course_number?";
chomp($course{$course_number} = <STDIN>);
print %course, "\n";
```

(Output)

```
What is the name of course 101? Linux Administration
101Linux Administration
```

### EXPLANATION

- 1 The hash, %course, is declared here. Keys and values will be assigned later.
- 2 The scalar variable $course_number is assigned the value 101.
- 3 The string What is the name of course 101? is printed to STDOUT.
- 4 The name of the hash is %course. We are assigning a value to one of the hash elements.
  The key is $course_number enclosed in curly braces. The chomp function will remove the newline from the value assigned by the user.
- 5 The new hash is printed. It has one key and one value.

### 10.2.7 Opening for Writing

When opening a file for writing, the file will be created if it does not exist, and if it already exists, it must have write permission. If the file exists, its contents will be overwritten. The filehandle is used to access the system file.

### FORMAT

```
open(my $filehandle, ">", "FILENAME"); # Three arguments, modern way
open(FILEHANDLE, ">FILENAME"); # Bareword, old way
```

### EXAMPLE 10.17

```
open($fh, ">", "temp");
open(PH, ">temp");
```

### EXPLANATION

- 1 The user-defined filehandle, $fh, will be used to send output to the file called temp. As with the shell, the redirection symbol directs the output from the default filehandle, STDOUT, to the temp file.
- 2 This is the two-argument older way to create a user-defined handle.
