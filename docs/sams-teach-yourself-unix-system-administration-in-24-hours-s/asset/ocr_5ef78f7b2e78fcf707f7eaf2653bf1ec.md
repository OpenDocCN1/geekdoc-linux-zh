> If you want to constrain your search to a single file system, add -xdev to the list of parameters.

2. I'll cast my net wider by looking across the entire file system, but because I know there are going to be lots of files, I'll just count lines the first time through:

```
# find / -user taylor -type f -ls | wc -l
686
```

To sum up the sizes of all files is a good job for awk or perl: I'll opt for awk because it's available on older Unix systems, too. The task we want is to have a script that extracts the seventh field of each line, then sums them all up and outputs the result. This can be done in awk with the succinct program

```
{ sum += $7 } END { print sum }
```

(the END tag denotes a block of instructions that is only run after all the lines have been read in).

```
# find / -user taylor -type f -ls | \
awk '{ sum += $7 } END { print sum }'
27869349
```

Let's see; that's in bytes, so dividing by 1024×1024 will reveal that this is 26 megabytes. Not too much disk space at all, even though the number certainly looks huge!

Of course, awk can do this math, too,

```
# find / -user taylor -type f -ls | \
awk '{ sum += $7 } END { print sum / (1024*1024) }'
26.5783
```