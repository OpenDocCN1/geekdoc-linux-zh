# FORMAT

```
number_of_bytes = read(FILEHANDLE, buffer, how_many_bytes);
```

# EXAMPLE 10.13

(The Script)

```
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

# EXPLANATION

+   The user is asked for input. If he types less than 10 characters, he should press <CTRL+D> to exit.

+   The read function takes three arguments: the first argument is STDIN, the place from where the input is coming; the second argument is the scalar $favorite, where the input will be stored; and the third argument is the number of characters (bytes) that will be read.

+   The 10 characters read in are printed. The rest of the characters were left in the buffer and ignored.

+   The number of characters (bytes) actually read was stored in $number and is finally printed.

# 10.2.4 Thegetc Function

Thegetc function gets a single character from the keyboard or from a file. At EOF,getc returns a null string.