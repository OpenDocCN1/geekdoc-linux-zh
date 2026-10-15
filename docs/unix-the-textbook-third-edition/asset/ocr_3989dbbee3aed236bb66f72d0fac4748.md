![](bbox=[0.38, 0.115, 0.72, 0.26])

# FIGURE 9.12 Semantics of the ls -l | more command.

```
[contents of temp]
$ rm temp
$
```

As you can see, not only do you need three commands to accomplish the same task, but the command sequence is also extremely slow because file read and write operations are involved. Recall that files are stored on a secondary storage device, usually a disk. On a typical contemporary computer system, disk operations are about one million times slower than main memory (random access memory [RAM]) operations. The actual performance gain in favor of pipes, however, is much smaller, owing to efficient caching of file blocks by the UNIX kernel and the use of semiconductor disks.

You can use the sort utility discussed in Chapter 7 to sort lines in a file. Suppose that you have a file called student_records that you want to sort and that the file may have some repeated lines that you want to appear only once in the sorted file. The sort -u student_records command can accomplish this task. As we discussed in Chapter 6, the uniq command can also do the task if it is given the sorted version of student_records with repeated lines in it. One way to perform the task is to use the following commands. The more command is used to show the contents of student_records.

```
$ more student_records
John Doe      ECE   3.54
Pam Meyer     CS    3.61
Jim Davis     CS    2.71
John Doe      ECE   3.54
Jason Kim     ECE   3.97
Amy Nash      ECE   2.38
$ sort student_records > student_records_sorted
$ uniq student_records_sorted
Amy Nash      ECE   2.38
Jason Kim     ECE   3.97
Jim Davis     CS    2.71
John Doe      ECE   3.54
Pam Meyer     CS    3.61
$
```

The same task can be accomplished in one command line by using a pipe, as follows:

```
$ sort student_records | uniq
Amy Nash      ECE   2.38
```