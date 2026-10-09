# **tip** unset: REMOVES A VARIABLE

Unless you remove a variable, it exists as long as the shell in which it was created exists. To remove the value of a variable but not the variable itself, assign a null value to the variable. In the following example, set (page 1024) displays a list of all variables and their values; grep extracts the line that shows the value of person.

```
$ echo $person
zach
$ person=
$ echo $person

$ set | grep person
person=
```

You can remove a variable using the unset builtin. The following command removes the variable person:

```
$ unset person
$ echo $person

$ set | grep person
$
```

# ## VARIABLE ATTRIBUTES

This section discusses attributes and explains how to assign attributes to variables.

# **readonly**: MAKES THE VALUE OF A VARIABLE PERMANENT

You can use the readonly builtin to ensure the value of a variable cannot be changed. The next example declares the variable person to be readonly. You must assign a value to a variable before you declare it to be readonly; you cannot change its value after the declaration. When you attempt to change the value of or unset a readonly variable, the shell displays an error message:

```
$ person=zach
$ echo $person
zach
$ readonly person
$ person=helen
bash: person: readonly variable
$ unset person
bash: unset: person: cannot unset: readonly variable
```

If you use the readonly builtin without an argument, it displays a list of all readonly shell variables. This list includes keyword variables that are automatically set as readonly as well as keyword or user-created variables that you have declared as readonly. See the next page for an example (readonly and declare -r produce the same output).