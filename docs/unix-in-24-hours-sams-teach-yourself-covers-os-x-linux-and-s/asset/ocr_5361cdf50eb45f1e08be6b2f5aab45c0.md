Click here to view code image

```
$ echo Joe is basically ${leaning:=pro }taxes and ${leaning}spending.
Joe is basically pro taxes and pro spending.
```

The first occurrence of the variable has it undefined, so the shell assigns "pro " (pro with a trailing space) to $leaning and outputs that. The second time the variable is interpreted, it has the value "pro ".

# 4. Variables are typically assigned within scripts but can also be assigned interactively by use of the read command. This assigns an individual word to a specified variable, with the last variable in the list being assigned the remaining words if there are more words entered than variables listed:

```
$ read city state message
CapeMay, New Jersey Hi Mom!
$ echo $city is city
CapeMay, is city
$ echo $state is state
New is state
$ echo $message is message
Jersey Hi Mom! is message
```

As you can see, only New is assigned to state. Frustrating!

The best way around this is to escape the space (make sure that the space isn’t interpreted as separating variable values) with a backslash:

Click here to view code image

```
$ read city state message
CapeMay, New\ Jersey Hi Mom!
$ echo $city is city
CapeMay, is city
$ echo $state is state
New Jersey is state
$ echo $message is message
Hi Mom! is message
```

This can be a bit tricky at first.

# 5. The third common way to assign variables is by using command-line arguments. The shell has built-in variables to access the command line. If you’ve written a script to copy files and named it copy-files, you might want to list all the files on the command line:

Click here to view code image

```
$ copy-files.sh file1 file2 file3
```

The program would access these arguments as $1, $2, and $3:

```
cp $1 destination
cp $2 destination
cp $3 destination
```

The $0 variable is a special case for looking at the command name, and $* lists all the command-line variables.

The standard data in any shell program is the variable. Such variables can be assigned in several ways: directly assigned, read in from a user’s typing, or assigned from the