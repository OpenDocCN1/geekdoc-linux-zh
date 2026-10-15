# 7.6 Variables

There are two types of variables: local and environment. Some variables are created by the user and others are special shell variables.

# 7.6.1 Local Variables

Local variables are given values that are known only to the shell in which they are created. Variable names must begin with an alphabetic or underscore character. The remaining characters can be alphabetic, decimal digits 0 to 9, or an underscore character. Any other characters mark the termination of the variable name. When assigning a value, there can be no whitespace surrounding the equal sign. To set the variable to null, the equal sign is followed by a newline.¹

A dollar sign is used in front of a variable to extract the value stored there.

Setting Local Variables. See Example 7.18 for a demonstration on setting a local variable.

# EXAMPLE 7.18

```
1
$ round=world
$ echo $round
world

2
$ name="Peter Piper"
$ echo $name
Peter Piper

3
$ x=
$ echo $x

4
$ file.bak="$HOME/junk"
file.bak=/home/jody/ellie/junk: not found
```

# EXPLANATION

+   1 The variable round is assigned the value world. When the shell encounters the dollar sign preceding a variable name, it performs variable substitution. The value of the variable is displayed.
+   
+   2 The variable name is assigned the value "Peter Piper". The quotes are needed to hide the whitespace so that the shell will not split the string into separate words when it parses the command line. The value of the variable is displayed.