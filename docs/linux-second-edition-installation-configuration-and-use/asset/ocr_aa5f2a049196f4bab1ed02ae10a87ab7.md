-d memory
limits the memory dedicated to the data segment of processes.

-f file.size
prevents creation of files larger than the specified limit. Only functions in the
ext2 file system.

-s memory
limits stack space.

# unalias abbreviation

unalias deletes an existing abbreviation. When the command is called with the op-
t-a, it deletes all known abbreviations.

# unset variable

unset deletes the specified variable.

```
until condition; do
commands
done
```

until is used for the construction of loops. The loop is executed until the specified
condition is satisfied. The criterion is the return value of the command specified as
the condition. Comparisons and tests are carried out with the command test or its
short notation in square brackets (see page 433).

```
wait [process.number]
```

wait waits for termination of the specified background process. When no process
number is specified, the command waits for termination of all running processes
started by the shell.

```
while condition; do
commands
done
```

while is used for the construction of loops. The loop is executed until the specified
condition is not satisfied for the first time. The criterion is the return value of the
command specified as the condition. Comparisons and tests are carried out with the
command test or its short notation in square brackets (see page 433).

# 13.7 Special characters reference

A large number of special characters can be used for various actions, both when en-
tering commands and when writing shell programs. The following table summarizes
all special characters dealt with Chapter IV (bash – a modern command interpreter)
and in this chapter.