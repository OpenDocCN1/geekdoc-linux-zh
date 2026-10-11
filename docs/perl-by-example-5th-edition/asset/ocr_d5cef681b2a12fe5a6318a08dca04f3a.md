# 10.2.2 The chop and chomp Functions

The *chop* function removes the last character in a scalar variable and the last character of each word in an array. Its return value is the character it chopped. *Chop* is used primarily to remove the newline from the line of input coming into your program, whether it is STDIN, a file, or the result of command substitution. When you first start learning Perl, the trailing newline can be a real pain!

The *chomp* function was introduced in Perl 5 to remove the last character in a scalar variable and the last character of each word in an array *only if* that character is the newline (or, to be more precise, the character that represents the input line separator, initially defined as a newline and stored in the `$/` variable). It returns the number of characters it chopped. Using *chomp* instead of *chop* protects you from inadvertently removing some character other than the newline.

# EXAMPLE 10.12

```
(The Script)
# Getting rid of the *trailing* newline. Use *chomp* instead of *chop*.
1 print "Hello there, and what is your name? ";
2 $name = <STDIN>;
3 print "$name is a very high class name.\n";
4 chop($name); # Removes the last character no matter what it is.
5 print "$name is a very high class name.\n";
6 chop($name);
7 print "$name has been chopped a little too much.\n";
8 print "What is your age? ";
9 $age=<STDIN>; # Removes the last character if
# it is the newline.
10 chomp($age); # The last character is not removed
# unless a newline.
11 print "For $age, you look so young!\n";

(Output)
1 Hello there, and what is your name? *Joe Smith*
3 Joe Smith
is a very high class name.
5 Joe Smith is a very high class name.
7 Joe Smit has been chopped a little too much.
8 What is your age? 25
11 For 25, you look so young!
```