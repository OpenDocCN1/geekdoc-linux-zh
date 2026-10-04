```
$ cat >lock
Ctrl-d
$ filecheck lock &
[1] 2364
$ rm lock
file lock does not exist...
```

Notice that the cat command in this example is just being used to create an empty file. There are other ways that this can be done. One of the simplest is to use the touch command. The actual purpose of this command is to update the timestamp on a file (given by ls -l) to the current time. However, as a side effect, using touch on a file that does not yet exist will create the file first as an empty file, and then update its timestamp:

```
$ ls -l lock
ls: lock: No such file or directory
$ touch lock
$ ls -l lock
-rw-r--r-- 1 pc book 0 Jul 3 21:52 lock
```

# 6.7.4 until Command

The until command is another looping construct. It is very similar to the while command, and has the general structure:

```
until condition
do
    commands
done
```

The difference between while and until is that while continues to loop for as long as its condition evaluates to true, whereas until does the opposite and continues to loop for as long as its condition evaluates to false. This would make the until command ideal if, for example, you needed a script to wait until a given file existed before it terminated:

```
until test -e $1
do
    sleep 2
done
echo file $1 now exists...
exit 0
```

Sometimes, you need to create a loop that goes round indefinitely. What is required for this is a command that always returns an exit status of zero (to make