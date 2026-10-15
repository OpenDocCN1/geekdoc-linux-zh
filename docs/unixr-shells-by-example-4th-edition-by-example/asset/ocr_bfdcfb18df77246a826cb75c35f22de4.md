# EXAMPLE 13.51

```
1 $ round=world or declare round=world
$ echo $round
world
2 $ name="Peter Piper"
$ echo $name
Peter Piper
3 $ x=
$ echo $x
4 $ file_bak="$HOME/junk"
bash: file_bak=/home/jody/ellie/junk: not found
```

# EXPLANATION

1 The local variable round is assigned the value world. When the shell encounters the dollar sign preceding a variable name, it performs variable substitution. The value of the variable is displayed. (Don't confuse the prompt $ with the $ used to perform variable substitution.)

2 The local variable name is assigned the value "Peter Piper". The quotes are needed to hide the whitespace so that the shell will not split the string into separate words when it parses the command line. The value of the variable is displayed.

3 The local variable x is not assigned a value. It will be assigned null. The null value, an empty string, is displayed.

4 The period in the variable name is illegal. The only characters allowed in a variable name are numbers, letters, and the underscore. The shell tries to execute the string as a command.

# EXAMPLE 13.52

```
1 $ echo $$
1313
2 $ round=world
$ echo $round
world
3 $ bash        # Start a subshell
4 $ echo $$
1326
5 $ echo $round
6 $ exit        # Exits this shell, returns to parent shell
7 $ echo $$
1313
8 $ echo $round
world
```