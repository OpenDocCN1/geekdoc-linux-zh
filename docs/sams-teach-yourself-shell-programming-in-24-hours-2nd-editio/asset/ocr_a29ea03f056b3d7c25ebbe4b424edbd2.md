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

# The until Loop

The while loop is perfect for a situation where you need to execute a set of commands while some condition is true, but sometimes you need to execute a set of commands until a condition is true. The until loop, available in ksh, bash and zsh, provides this functionality. Its syntax is

```
until cmd
do
  list
done
```

Here cmd is a single command, whereas list is a set of one or more commands. Although cmd can be any valid UNIX command, it is usually a test expression of the type covered in Chapter 11, "Flow Control."

The execution of an until loop is similar to that of the while loop:

+   1. Execute cmd.
+   2. If the exit status of cmd is nonzero, exit from the until loop.
+   3. If the exit status of cmd is zero, execute list.
+   4. When list finishes executing, return to Step 1.

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