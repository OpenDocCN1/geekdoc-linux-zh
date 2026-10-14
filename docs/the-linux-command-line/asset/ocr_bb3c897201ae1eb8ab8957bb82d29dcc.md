If we perform this sequence, the result will be nothing, because the shell will try to expand a variable named a_file rather than a. This problem can be solved by adding braces:

```
[me@linuxbox ~]$ echo "${a}_file"
foo_file
```

We have also seen that positional parameters greater than 9 can be accessed by surrounding the number in braces. For example, to access the eleventh positional parameter, we can do this:

${11}

# Expansions To Manage Empty Variables

Several parameter expansions deal with nonexistent and empty variables. These expansions are handy for handling missing positional parameters and assigning default values to parameters.

${parameter:-word}

If parameter is unset (i.e., does not exist) or is empty, this expansion results in the value of word. If parameter is not empty, the expansion results in the value of parameter.

```
[me@linuxbox ~]$ foo=
[me@linuxbox ~]$ echo ${foo:-"substitute value if unset"}
substitute value if unset
[me@linuxbox ~]$ echo $foo

[me@linuxbox ~]$ foo=bar
[me@linuxbox ~]$ echo ${foo:-"substitute value if unset"}
bar
[me@linuxbox ~]$ echo $foo
bar
```

${parameter:=word}

If parameter is unset or empty, this expansion results in the value of word. In addition, the value of word is assigned to parameter. If parameter is not empty, the expansion results in the value of parameter.

```
[me@linuxbox ~]$ foo=
[me@linuxbox ~]$ echo ${foo:="default value if unset"}
```