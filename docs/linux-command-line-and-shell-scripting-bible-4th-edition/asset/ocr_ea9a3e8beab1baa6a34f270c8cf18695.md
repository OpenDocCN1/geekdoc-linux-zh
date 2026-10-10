for most commands, if you run lots of scripts from your shell scripts, it
could be useful:

```
$ cat can-I-run-it.sh
#!/bin/bash
# Check if you can run a file
#
item_name=$HOME/scripts/can-I-write-to-it.sh
echo
echo "Checking if you can run $item_name..."
#
# Check if file is executable.
#
if [ -x $item_name ]
then
        echo "You can run $item_name."
        echo "Running $item_name..."
        $item_name
#
else
        echo "Sorry, you cannot run $item_name."
#
fi
$
$ ./can-I-run-it.sh

Checking if you can run /home/christine/scripts/can-I-write-
to-it.sh...You can run /home/christine/scripts/can-I-write-to-it.sh.
Running /home/christine/scripts/can-I-write-to-it.sh... [...] 
$
$ chmod u-x can-I-write-to-it.sh
$
$ ./can-I-run-it.sh

Checking if you can run /home/christine/scripts/can-I-write-
to-it.sh... Sorry, you cannot run /home/christine/scripts/can-I-write-
to-it.sh.
$
```

This example shell script uses the -x comparison to test whether you
have permission to execute the can-I-write-to-it.sh script. If so, it
runs the script. After successfully running the can-I-write-to-it.sh
script the first time, the permissions were changed. This time, the -x