# Variables 99

Variables can be used anywhere on any command line and will be replaced with their value by the shell prior to the specific command invoked, as the next examples illustrate:

```
$ ls $my_bin
mon
u
testx
$ pwd
/users/steve/documents/memos
$ cd $my_bin
$ pwd
/users/steve/bin
$ number=99
$ echo There are $number bottles of beer on the wall
There are 99 bottles of beer on the wall
$
```

Where are we?

Change to my bin directory

Here are some more examples:

```
$ command=sort
$command names
Charlie
Emanuel
Fred
Lucy
Ralph
Tony
Tony
$ command=wc
$ option-l
$ file=names
$command $option $file
7 names
```

So you see, even the name of a command can be stored inside a variable. Because the shell performs its substitution before determining the name of the program to execute and its arguments, it parses the line

```
$command $option $file
```

then makes all the substitutions requested, turning the command it actually invokes into

```
wc -l names
```

Then the shell can be assigned to other variables, as shown in the next example:

```
$ value1=10
$ value2=$value1
$ echo $value2
```