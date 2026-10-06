# Part IV Alternative Linux Shells

```
echo "Hello world!"
breaksw
case exit:
  echo "Thank you for playing"
breaksw
default:
  echo "Sorry, I don't understand that command"
endsw
$ ./test9
Please enter a word: test
This is a test
$ ./test9
Please enter a word: testing
Sorry, I don't understand that command
$ ./test9
Please enter a word: exit
Thank you for playing
$
```

Since the tcsh shell does not include a read statement like the bash shell, you must read an input value directly from STDIN. You do this using the $< symbol.

```
set input = $<$
```

After retrieving the input, the switch statement compares the text to each case statement. If no match, it uses the default statement (if provided).

> In case you were wondering, the tcsh shell doesn't support functions in shell scripts. This can be a huge hindrance when converting bash shell scripts for the tcsh environment.

# Summary

This chapter discussed the features found in the C shell. While the C shell is not overly popular in the Linux world, you may still run into it, so it's a good idea to know how it differs from the bash shell.

The most popular C shell implementation is the tcsh shell. While the tcsh shell is usually not the default shell in Linux, it's usually available as an installation file. This allows you to write and test scripts used in a Unix environment that uses the C shell.

The C shell uses two types of variables, shell variables and environment variables. Shell variables are lower case and contain system information and settings commonly used in the C shell. The environment variables are mostly used for compatibility with Bourne and bash shell scripts, and maintain simple values such as the path and shell name.