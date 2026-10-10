# Part II: Shell Scripting Basics

# ## Viewing jobs

The key command for job control is the `jobs` command. The `jobs` command allows you to view the current jobs being handled by the shell. Though it doesn't contain the `jobs` command, the following script demonstrates the command's power:

```
```bash
$ cat jobcontrol.sh
#!/bin/bash
#Testing job control
# echo "Script Process ID: $$"
# count=1
# while [ $count -le 5 ]
# do
#       echo "Loop #$count"
#       sleep 10
#       count=$[ $count + 1 ]
# done
# echo "End of script..."
# exit
$ ````
```

The script uses the $ variable to display the PID that the Linux system assigns to the script; then it goes into a loop, sleeping for 10 seconds at a time for each iteration.

You can start the script from the command-line interface and then stop it using the `Ctrl+Z` key combination:

```
```
$ ./jobcontrol.sh
Script Process ID: 1580
Loop #1
Loop #2
Loop #3
^Z
[1]+  Stopped
$                  ./jobcontrol.sh
````
```

Using the same script, another job is started as a background process, using the ampersand symbol. To make life a little easier, the output of that script is redirected to a file so that it doesn't appear on the screen:

```
```
$ ./jobcontrol.sh > jobcontrol.out &
[2] 1603
$ 
````
```

The `jobs` command enables you to view the jobs assigned to the shell, as shown here:

```
```
$ jobs
[1]+  Stopped
$                  ./jobcontrol.sh
[2]-  Running
$                  ./jobcontrol.sh > jobcontrol.out & 
````
```

382