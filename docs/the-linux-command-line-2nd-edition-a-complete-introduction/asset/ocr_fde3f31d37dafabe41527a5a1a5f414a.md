# 29 – Flow Control: Looping With while / until

tial order from one to five. a bash script could be constructed as follows:

```
#!/bin/bash

# while-count: display a series of numbers

count=1

while [[ $count -le 5 ]]; do
    echo $count
    count=$((count + 1))
done
echo "Finished."
```

When executed, this script displays the following:

```
[me@linuxbox ~]$ while-count
1
2
3
4
5
Finished.
```

The syntax of the while command is:

```
while commands; do commands; done
```

Like if, while evaluates the exit status of a list of commands. As long as the exit status is zero, it performs the commands inside the loop. In the script above, the variable count is created and assigned an initial value of 1. The while command evaluates the exit status of the test command. As long as the test command returns an exit status of zero, the commands within the loop are executed. At the end of each cycle, the test command is repeated. After six iterations of the loop, the value of count has increased to 6, the test command no longer returns an exit status of zero and the loop terminates. The program continues with the next statement following the loop.

We can use a while loop to improve the read-menu program from the previous chapter:

```
#!/bin/bash

# while-menu: a menu driven system information program
```