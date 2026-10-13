
## while and Subshells

A problem with the loop used in the previous example is that it is executed in a subshell in Bourne shell and older versions of ksh. This means that any changes to the script environment, such as exporting variables and changing the current working directory, might not be present after the while loop completes. As an example, consider the following script:

```
#!/bin/sh
if [ -f "$1" ] ; then
i=0
while read LINE
do
i=`expr $i + 1`
done < "$1"
echo $i
fi
```

This script tries to count the number of lines in the file specified to it as an argument.

Executing this script on the file

```
$ cat dirs.txt
/tmp
/usr/local
/opt/bin
/var
```

can produce the following incorrect result:

0

Although you are incrementing the value of $i using the command i=`expr $i + 1` when the while loop completes, the value of $i is not preserved. In this case, you need to change a variable's value inside the while loop and then use that value outside the loop. One way to solve this problem is to redirect STDIN prior to entering the loop and then restore STDIN after the loop completes. The basic syntax is

```
exec n<&0 < file
while read LINE
do
: # manipulate file here
done
exec 0<&n
```

Here, n is an integer greater than 2, and file is the name of the file you want to read. Usually n is chosen as a small number such as 3, 4, or 5. This allows you to construct a shell version of the cat command as follows:

```
#!/bin/sh
if [ $# -ge 1 ] ; then
  for FILE in "$@"
  do
    exec 4<&0 < "$FILE"
    while read LINE ; do echo $LINE ; done
    exec 0<&4 4<&-
  done
fi
```

## The until Loop

The while loop is perfect for a situation where you need to execute a set of commands while some condition is true, but sometimes you need to execute a set of commands until a condition is true. The until loop, available in ksh, bash and zsh, provides this functionality. Its syntax is

```
until cmd
do
  list
done
```

Here cmd is a single command, whereas list is a set of one or more commands. Although cmd can be any valid UNIX command, it is usually a test expression of the type covered in Chapter 11, "Flow Control."

The execution of an until loop is similar to that of the while loop:

- 1. Execute cmd.
- 2. If the exit status of cmd is nonzero, exit from the until loop.
- 3. If the exit status of cmd is zero, execute list.
- 4. When list finishes executing, return to Step 1.

If both cmd and list are short, the until loop can be written on a single line as follows:

```
until cmd ; do list ; done
```

In most cases an until loop is identical to a while loop with cmd negated using the ! operator. For example, the following while loop

```
x=1
while [ ! $x -ge 10 ]
do
  echo $x
  x=`expr $x + 1`
done
```

is equivalent to the following until loop:

```
x=1;
until [ $x -ge 10 ]
do
  echo $x
  x=`expr $x + 1`
done
```

The until loop offers no advantages over the equivalent while loop. Because it isn't supported by the Bourne shell, most programmers do not favor it. It is covered here for the sake of completeness.

## The for and select Loops

Unlike the while loop, which exits when a certain condition is false, the for and select loops operate on lists of items. This section covers these two loops in detail.

### The for Loop

The for loop enables you to execute a set of commands repeatedly for each item in a list. One of its most common uses is in performing the same set of commands for a large number of files. The basic syntax is

```
for name in word1 word2 ... wordN
do
  list
done
```

Here name is the name of a variable and word1 to wordN are sequences of characters separated by spaces (words). Each time the for loop executes, the value of the variable name is set to the next word in the list of words, word1 to wordN. The first time, name is set to word1; the second time, it's set to word2; and so on. This means that the number of times a for loop executes depends on the number of words that are specified. For example, if the following words were specified to a for loop

there comes a time

the loop would execute four times. In each iteration of the for loop, the commands specified in list are executed.

A for loop can be written on a single line as follows:

for name in word1 word2 ... wordN ; do list ; done

If list and the number of words are short, the single line form is often chosen; otherwise, the multiple-line form is preferred.

A simple for loop example is

```
for i in 0 1 2 3 4 5 6 7 8 9
do
  echo $i
done
```

This loop counts to nine as follows:

- 0
- 1
- 2
- 3
- 4
- 5
- 6
- 7
- 8
- 9

Note that although the output is identical to the while loop, the for loop does something altogether different. In each iteration, $i is set to the next item in the list. When the list is finished, the loop exits. In this example, you chose the list to be the numbers from 0 to 9. In the while loop, the next number to display was being computed, and it was not part of a predetermined list.

If you change the list slightly, notice how the output changes:

```
for i in 0 1 2 4 3 5 8 7 9
do
  echo $i
done
```

- 0
- 1
- 2
- 4
- 3
- 5
- 8
- 7
- 9

### Manipulating a Set of Files

Say that you need to copy a bunch of files from one directory to another and change the permissions on the copy. You could do this by copying each file and changing the permissions manually.

This is what we were interested in. In fact this is one of the most common uses of the for loop—iterating over a set of filenames and performing some operations on those files.

The procedure to do this follows:

- 1. Create a for loop with a variable named file or FILE. Other favored names include i, j, and k. The name of the variable is usually singular.
- 2. Create a list of files to manipulate. This is frequently accomplished using the file-name substitution technique discussed in Chapter 9, "Substitution."
- 3. Manipulate the files in the body of the loop.

An example of this is the following for loop:

```
for FILE in $HOME/.bash*
 do
  cp $FILE $HOME/public_html
  chmod a+r $HOME/public_html/$FILE
 done
```

In this loop, you use filename substitution to obtain a list of files in your home directory that start with .bash*. In the body of the loop, each of these files is copied to the directory public_html and made readable by everyone.

### The select Loop

The select loop provides an easy way to create a numbered menu from which users can select options. It is useful when you need to ask the user to choose one or more items from a list of choices. The select loop was introduced in ksh and has been adapted by bash and zsh. It is not available in the Bourne shell.

The basic syntax of the select loop is

```
select name in word1 word2 ... wordN
 do
  list
 done
```

Here name is the name of a variable and word1 to wordN are sequences of characters separated by spaces (words). The set of commands to execute after the user has made a selection is specified by list.

The execution process of a select loop is as follows:

- 1. Each item in list is displayed along with a number.
- 2. A prompt, usually #?, is displayed.
- 3. When the user enters a value, $REPLY is set to that value.
- 4. If $REPLY contains a number of a displayed item, the variable specified by name is set to the item in list that was selected. Otherwise, the items in list are displayed again.
- 5. When a valid selection is made, list executes.
- 6. If list does not exit from the select loop using one of the loop control mechanisms such as break, the process starts over at Step 1.

If the user enters more than one valid value, $REPLY contains all the user's choices. In this case, the variable specified by name is not set.

### An Example of the select Loop

One common use of the select loop is in scripts that configure software. The following example is a simplified version of one such script. The actual configuration commands have been omitted because they are not relevant in this discussion.

```
select COMPONENT in comp1 comp2 comp3 all none
do
  case $COMPONENT in
    comp1|comp2|comp3) CompConf $COMPONENT ;;
    all) CompConf comp1
         CompConf comp2
         CompConf comp3
         ;;
    none) break ;;
    *) echo "ERROR: Invalid selection, $REPLY." ;;
  esac
done
```

The menu presented by the select loop looks like the following:

```
1) comp1
2) comp2
3) comp3
4) all
5) none
#?
```

As you can see, each of the items in the list comp1 comp2 comp3 all none are displayed with a number preceding them. The user can enter one of these numbers to select a particular component. If a valid selection is made, the select loop executes a case statement contained in its body. This case statement performs the correct action based on the user's input. Here the correct action is either calling a command named CompConf, exiting the loop, or displaying an error message.
