
You can also set the -x option of the shell running the script by putting the following set x command near the beginning of the script:

set -x

Put set -x anywhere in the script you want to turn debugging on. Turn the debugging off with a plus sign:

set +x

The set -o xtrace and +o xtrace commands do the same things as set -x and set +x, respectively.

## for...in

The for...in control structure has the following syntax:

+   for loop-index in argument-list
  do
    commands
  done

![](img/45ff4cd21497435daa35084a84b95d07_1017_0.png)

Figure 27-4 A for...in flowchart

The for...in structure (Figure 27-4, previous page) assigns the value of the first argument in the argument-list to the loop-index and executes the commands between the do and done statements. The do and done statements mark the beginning and end of the loop.

After it passes control to the done statement, the structure assigns the value of the second argument in the argument-list to the loop-index and repeats the commands. It repeats the commands between the do and done statements one time for each argument in the argument-list. When the structure exhausts the argument-list, it passes control to the statement following done.

The following for...in structure assigns apples to the user-created variable fruit and displays the value of fruit, which is apples. Next the structure assigns oranges to fruit and repeats the process. When it exhausts the list, the structure transfers control to the statement following done, which displays a message.

+   $ cat fruit
for fruit in apples pears bananas

```
do
echo "$fruit"
done
echo "Task complete."
```

+   $ ./fruit
apples
oranges
pears
bananas
Task complete.

The next script lists the names of the directory files in the working directory by looping through the files in the working directory and using test to determine which are directory files:

+   $ cat dirfiles

```
for i in *
do
if [ -d "$i" ];
then
echo "$i"
done
```

The ambiguous file reference character * matches the names of all files (except hidden files) in the working directory. Prior to executing the for loop, the shell expands the * and uses the resulting list to assign successive values to the index variable i.

The for control structure has the following syntax:

```
for loop-index
do
commands
done
```

## CONTROL STRUCTURES 969

In the for structure, the loop-index takes on the value of each command-line argument, one at a time. The for structure is the same as the for...in structure (Figure 27-4, page 967) except in terms of where it gets values for the loop-index. The for structure performs a sequence of commands, usually involving each argument in turn.

The following shell script shows a for structure displaying each command-line argument. The first line of the script, for arg, implies for arg in "$@", where the shell expands "$@" into a list of quoted command-arguments "$1" "$2" "$3" and so on. The balance of the script corresponds to the for...in structure.

```
$ cat for_test
for arg
do
  echo "$arg"
done
$ for_test candy gum chocolate
  candy
  gum
  chocolate
```

## optional THE whos SCRIPT

The following script, named whos, demonstrates the usefulness of the implied "$@" in the for structure. You give whos one or more users' full names or usernames as arguments, and whos displays information about the users. The whos script gets information from the first and fifth fields in the /etc/passwd file. The first field contains a username, and the fifth field typically contains the user's full name. You can provide a username as an argument to whos to identify the user's name or provide a name as an argument to identify the username. The whos script is similar to the finger utility, although whos delivers less information.

```
$ whos
!/bin/bash

if [ $# -eq 0 ];
then
  echo "Usage: whos id..." 1>&2
  exit 1
fi
for id
do
  awk -F: '{print $1, $5}' /etc/passwd |
  grep -i "$id"
done
```

In the next example, whos identifies the user username is chas and the user name is Marilou Smith:

```
$ ./whos chas "Marilou Smith"
chas Charles Casey
smith Marilou Smith
```

Use "$@" The script uses a for statement to loop through the command-line arguments. In this script the implied use of "$@" in the for loop is particularly beneficial because it causes the loop to treat an argument that contains SPACE as a single argument. This encloses Marilou Smith in quotation marks, which causes the shell to pass it to the script as a single argument. The implied "$@" in the for statement causes the shell to regenerate the quoted argument Marilou Smith so that it is treated as a single argument.

awk For each command-line argument, which searches the /etc/passwd file. Inside the for loop, the awk utility extracts the first ($1) and fifth ($5) fields from each line in /etc/passwd. The -F option causes awk to use a colon (:) as a field separator when it reads /etc/passwd, allowing it to break each line into fields. The awk command sets the following-

## while

The while control structure has the following syntax:

+   while test-command
  do
    commands
  done

As long as the test-command returns true, the structure executes the commands between the do and done statements. When the exit status of the test-command is false, the structure passes control to the statement after done.

## CONTROL STRUCTURES 971

![](img/45ff4cd21497435daa35084a84b95d07_1021_0.png)

executes the commands between the do and done statements. See page 955 for information on the test builtin.

```
$ cat count
!/bin/bash
number=0
while [ "$number" -lt 10 ]
  do
    echo -n "$number"
    ((number +=1))
  done
$ ./count
0123456789
$
```
