# LAB 15
Turning Commands into a Script: Shell Scripting

**Lab Objective:**
Learn how to write a simple shell script containing multiple commands.

**Lab Purpose:**
Scripting with Bash is a daily task by many professional Linux administrators. When a task is repetitive, you don’t want to be typing the same list of commands over and over; you want to create a script, and perhaps also schedule that script to run automatically.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

*Task 1:*
Open the Terminal application, and run your favorite text editor, such as `vi` or `nano`. (If you have never used `vi` or `vim`, then `nano` is strongly recommended.)

Create a file with the following contents:

```
#!/bin/bash
for (( n=0; n<$1; n++ ))
do
    echo $n
done
echo "Output from $0 complete."
```

*Task 2:*
Make the file executable (with `chmod +x filename`), then run it like:

```
./filename 10
```