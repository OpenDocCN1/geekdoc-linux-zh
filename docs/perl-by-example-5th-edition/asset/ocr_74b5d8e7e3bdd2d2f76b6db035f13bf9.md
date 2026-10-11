```
(The Script)

```per
use warnings;
# Assigning input to an array
1 print "Tell me everything about yourself.\n";
2 my @all = <STDIN>;
3 print "all";
4 print "The number of elements in the array are: ",
      $all + 1, "\n";
5 print "The first element of the array is: $all[0]";
```
```

The Script

```
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

+   1 Tell me everything about yourself.
+   2 OK. Let’s see I was born before computers.
+   I grew up in the 50s.
+   I was in the hippie generation.
+   I’m starting to get bored with talking about myself.
+   <CTRL>+D
+   3 OK. Let’s see I was born before computers.
+   I grew up in the 50s.
+   I was in the hippie generation.
+   I’m starting to get bored with talking about myself.
+   4 The number of elements in the array are: 4.
+   5 The first element of the array is:
+   OK. Let’s see I was born before computers.

# EXPLANATION

+   1 The string *Tell me everything about yourself.* is printed to STDOUT.
+   2 The input operator <> surrounding STDIN reads input lines until <CTRL>+D. EOF, is reached. (For Windows, use <CTRL>+Z instead of <CTRL>+D.) Each line and its trailing newline are stored as a list element of the array @all.
+   3 The user input is printed to the screen after the user presses <CTRL>+D or <CTRL>+Z.
+   4 The $# construct lets you get the last subscript or index value in the array. By adding 1 to $#all, the size of the array is obtained; that is, the number of lines that were read.
+   5 $all[0] is the first element of the array that evaluates to the first line of input from the user. Each line read is an element of the array.

# 10.2.6  Assigning Input to a Hash

Reading input from STDIN and assigning it to a hash is like reading from a file. The line read can be assigned as a value corresponding to a hash key or as the key itself.