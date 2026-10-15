
## 13.10 Variables

```
declare variable=value
```

```
declare name=Tommy
```

**Table 13.13** declare Options

| Option | Meaning |
|---|---|
| `-a` | Treats variable as an array (i.e., assigns elements) |
| `-f` | Lists functions names and definitions |
| `-fa` | Lists just function names |
| `-i` | Makes variables integer types |
| `-r` | Makes variables read-only |
| `-x` | Exports names to subshells |

a. `-a` and `-F` are implemented only on versions of bash 2.x.

### 13.10.4 Local Variables and Scope

The scope of a variable refers to where the variable is visible within a program. For the shell, the scope of local variables is confined to the shell in which the variable is created.

When assigning a value, there can be no whitespace surrounding the equal sign. To set the variable to null, the equal sign is followed by a newline.⁹

A dollar sign is used in front of a variable to extract the value stored there.

The local function can be used to create local variables, but this is only used within functions. (See “Defining Functions” on page 841.)

**Setting Local Variables.** Local variables can be set by simply assigning a value to a variable name, or by using the declare built-in function as shown in Example 13.51.

9. A variable set to a value or to null will be displayed by using the set command, but an unset variable will not.

## EXAMPLE 13.51

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

## EXPLANATION

1 The local variable round is assigned the value world. When the shell encounters the dollar sign preceding a variable name, it performs variable substitution. The value of the variable is displayed. (Don't confuse the prompt $ with the $ used to perform variable substitution.)

2 The local variable name is assigned the value "Peter Piper". The quotes are needed to hide the whitespace so that the shell will not split the string into separate words when it parses the command line. The value of the variable is displayed.

3 The local variable x is not assigned a value. It will be assigned null. The null value, an empty string, is displayed.

4 The period in the variable name is illegal. The only characters allowed in a variable name are numbers, letters, and the underscore. The shell tries to execute the string as a command.

## EXAMPLE 13.52

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

## EXPLANATION

+   1 The value of the double dollar sign variable evaluates to the PID of the current shell. The PID of this shell is 1313.
+   2 The local variable round is assigned the string value world, and the value of the variable is displayed.
+   3 A new bash shell is started. This is called a subshell, or child shell.
+   4 The PID of this shell is 1326. The parent shell's PID is 1313.
+   5 The local variable round is not defined in this shell. A blank line is printed.
+   6 The exit command terminates this shell and returns to the parent shell. (Ctrl-D will also exit this shell.)
+   7 The parent shell returns. Its PID is displayed.
+   8 The value of the variable round is displayed. It is local to this shell.

Setting Read-Only Variables. A read-only variable is a special variable that cannot be redefined or unset. If, however, the declare function is used, a read-only variable can be redefined, but not unset.

## EXAMPLE 13.53

```
1 $ name=Tom
2 $ readonly name
$ echo $name
Tom

3 $ unset name
bash: unset: name: cannot unset: readonly variable
4 $ name=Joe
bash: name: readonly variable

5 $ declare -r city='Santa Clara'
6 $ unset city
bash: unset: city: cannot unset: readonly variable

7 $ declare city='San Francisco'  # what happened here?
$ echo $city
San Francisco
```

## EXPLANATION

+   1 The local variable name is assigned the value Tom.
+   2 The variable is made read-only.
+   3 A read-only variable cannot be unset.
+   4 A read-only variable cannot be redefined.
