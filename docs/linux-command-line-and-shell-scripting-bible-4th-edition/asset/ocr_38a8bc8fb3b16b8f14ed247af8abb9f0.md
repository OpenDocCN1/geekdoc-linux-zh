```
while [ $count -le 5 ]
do
   echo "loop #$count"
   sleep 1
   count=$[ $count + 1 ]
done
#
echo "Script is completed."
exit
$
$ ./backgroundoutput.sh &
[1] 2615
$ Starting the script...
Loop #1
Loop #2
Loop #3
Loop #4
Loop #5
Script is completed.

[1]+  Done              ./backgroundoutput.sh
$
```

You'll notice from the example that the output from the backgroundoutput.sh script displays. The output intermixes with the shell prompt, which is why Starting the script appears next to the $ prompt.

You can still issue commands while this output is occurring:

```
$ ./backgroundoutput.sh &
[1] 2719
$ Starting the script...
Loop #1
Loop #2
Loop #3
pwd
/home/christine/scripts
$ Loop #4
Loop #5
Script is completed.

[1]+  Done              ./backgroundoutput.sh
$
```

While the backgroundoutput.sh script is running in the background, the command pwd was entered. The script's output, the typed