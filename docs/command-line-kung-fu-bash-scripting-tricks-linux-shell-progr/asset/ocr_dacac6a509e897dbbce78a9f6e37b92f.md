```
$ cat cities.csv | cut -d, -f2

"Chicago"
"Austin"
"Santa Cruz"
$ cat cities.csv | cut -d, -f2 | tr -d ','

Chicago
Austin
Santa Cruz
$ 
```

You can also let tr delete a group of characters. This example removes all the vowels from the output.

```
$ cat cities.csv | cut -d, -f2 | tr -d [aeiou]
"Chcgo"
"Astin"
"Snt Crz"
$ 
```

# Count the Number of Occurrences of a String

```
$ uniq -c file
$ command | uniq -c
```

The uniq command omits adjacent duplicate lines from files. Since uniq doesn't examine an entire file or stream of input for unique lines, only unique adjacent lines, it is typically preceded by the sort command via a pipe. You can have the uniq command count the unique occurrences of a string by using the “-c” option. This comes in useful if you are trying to look through log files for occurrences of the same message, PID, status