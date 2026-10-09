Here the child process inherits the value of **cheese** as **american** and, after displaying this value, changes *its copy* to **swiss**. When control is returned to the parent, the parent's copy of **cheese** retains its original value: **american**.

Alternatively, as the next program shows, you can put a variable in the environment of a child shell without declaring it in the parent shell. See page 148 for more information on this command-line syntax.

```
```
$ cheese=cheddar ./substest
./substest 1: cheddar
./substest 2: swiss
$ echo $cheese
$ 
```
```

You can export a variable without/before assigning a value to it. Also, you do not need to export an already-exported variable after you change its value. For example, you do not usually need to **export PATH** when you assign a value to it in ~/.bash_profile because it is typically exported in a global startup file.

You can place several **export** declarations (initializations) on a single line:

```
```
$ export cheese=swiss coffee=colombian avocados=us
```
```

An **export -n** or **declare +x** command removes the export attribute from the named environment variable (unexports the variable), demoting it to become a shell variable while preserving its value.

An **export -f** command places the named function (page 396) in the environment so it is available to child processes.

# printentv: DISPLAYS ENVIRONMENT VARIABLE NAMES AND VALUES

The **printentv** utility displays environment variable names and values. When called without an argument, it displays all environment variables. When called with the name of an environment variable, it displays the value of that variable. When called with the name of a variable that is not in the environment or has not been declared, it displays nothing. You can also use **export** (page 1032) and **env** (next page) to display a list of environment variables.

```
```
$ x=5                  # not in the environment
$ export y=10          # in the environment
$ printentv x
$ printentv y
10
$ printentv
...
SHELL=/bin/bash
TERM=xterm
USER=sam
PWD=/home/sam
y=10
...
```
```