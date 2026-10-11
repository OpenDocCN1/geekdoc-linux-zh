```
```
for state in `cat $myfile`
do
echo "I am planning to continue my travel circle across the United States in the summer. The
next state I will visit is $state"
done
```

Alabma
Alaska
Arizoma
Arkansas
Califomnia
Colorado
Delaware
Florida
Georgia
Idaho
Iowa
Kansas
Kentucky
Maine
Michigan
Minnesota
Missouri
Montana
Nebaska
Ohio
Oregom
Tennesse
Texas
Utah
Vermont
Virgina
```

# **The while Command**

The while command is a cross between the if-then statement and Linux for loop. It allows you to define a command to test a condition and then looping through a set of commands until you reach a zero exit status. It will analyze the test command at the start of each iteration. Upon reaching the non-zero exit status, the while command stops the execution of the set of commands.

```
```
$ cat test10
#!/bin/bash
# This is a while command test in Linux
var15=20
while [ $var15 -gt 0 ]
do
echo This is $var15 in the while loop.
var15=[$var15 - 1 ]
done

$ bash -f main.sh
This is 20 in the while loop.
This is 19 in the while loop.
```
```