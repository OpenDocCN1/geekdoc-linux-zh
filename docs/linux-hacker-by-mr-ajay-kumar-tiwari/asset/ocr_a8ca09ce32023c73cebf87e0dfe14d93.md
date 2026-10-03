# Linux Hack

Ajay Kumar Tiwari

# Hack 19. Suppress Standard Output and Error Message

Sometime while debugging a shell script, you may not want to see either the standard output or standard error message. Use /dev/null as shown below for suppressing the output.

# Suppress standard output using > /dev/null

This will be very helpful when you are debugging shell scripts, where you don’t want to display the echo statement and interested in only looking at the error messages.

```
# cat file.txt > /dev/null
```

```
# ./shell-script.sh > /dev/null
```

# Suppress standard error using 2> /dev/null

This is also helpful when you are interested in viewing only the standard output and don’t want to view the error messages.

```
# cat invalid-file-name.txt 2> /dev/null
```

```
# ./shell-script.sh 2> /dev/null
```

# Hack 20. Join Command

Join command combines lines from two files based on a common field.

In the example below, we have two files – employee.txt and salary.txt. Both have employee-id as common field. So, we can use join command to combine