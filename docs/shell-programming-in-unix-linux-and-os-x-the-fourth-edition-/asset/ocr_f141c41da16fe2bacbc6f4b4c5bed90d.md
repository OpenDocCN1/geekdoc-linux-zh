So one colon or several consecutive colons on the input will be replaced by a *single* tab character on the output.

Note that `\t` can work in many instances instead of `\11`, so be sure to try that if you want things to be a bit more readable!

Suppose that you have a file called `lotsaspaces` that has contents as shown:

```
```text
$ cat lotsaspaces
This       is       an example of a
file    that contains    a lot
of   blank spaces.
$
```
```

You can use `tr` to squeeze out the multiple spaces by using the `-s` option and by specifying a single space character as the first and second argument:

```
```text
$ tr -s ' ' ' ' < lotsaspaces
This is an example of a
file that contains a lot
of blank spaces.
$
```
```

This `tr` command in effect says, “translate occurrences of space with another space, replacing multiple spaces in the input with a single space.”

# The `-d` Option

`tr` can also be used to delete individual characters from the input stream. The format of `tr` in this case is

```
```text
tr -d from-chars
```
```

where any character listed in `from-chars` will be deleted from standard input. In the following example, `tr` is used to delete all spaces from the file `intro`:

```
```text
$ tr -d ' ' < intro
TheUNIXOperatingSystemwaspioneeredbyKen
ThompsonandDennisRitchieatBellLaboratories
inthelate1960s.Oneoftheprimarygoalsin
thedesignoftheUNIXSystemwastocreatean
environmentthatpromotedefficientprogram
development.
$
```
```

You probably realize that you could have also used `sed` to achieve the same results:

```
```text
$ sed 's/ //g' intro
TheUNIXOperatingSystemwaspioneeredbyKen
ThompsonandDennisRitchieatBellLaboratories
inthelate1960s.Oneoftheprimarygoalsin
thedesignoftheUNIXSystemwastocreatean
environmentthatpromotedefficientprogram
```
```