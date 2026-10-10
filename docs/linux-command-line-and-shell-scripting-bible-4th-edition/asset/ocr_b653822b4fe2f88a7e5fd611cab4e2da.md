```
```
$ ls -al
total 72
drwxr-xr-x    3 rich    rich          4096 Jun 21 22:20 ./
drwxr-xr-x    9 rich    rich          4096 Jun 21 09:44 ../
drwx------    2 rich    rich          4096 Jun 21 22:20
dir.out8S8/
-rwxr--r--    1 rich    rich           338 Jun 21 22:20
test21
$ cd dir.out8S8
[dir.out8S8]$ ls -al
total 16
drwx------    2 rich    rich          4096 Jun 21 22:20 ./
drwxr-xr-x    3 rich    rich          4096 Jun 21 22:20 ../
-rw-------    1 rich    rich            44 Jun 21 22:20
temp.N5F306
-rw-------    1 rich    rich            44 Jun 21 22:20
temp.SQslb7
[dir.out8S8]$ cat temp.N5F306
This is a test line of data for temp.N5F306
[dir.out8S8]$ cat temp.SQslb7
This is a test line of data for temp.SQslb7
[dir.out8S8]$
```
```

The script creates a directory in the current directory and uses the `cd` command to change to that directory before creating two temporary files. The two temporary files are then assigned to file descriptors and used to store output from the script.

# # Logging Messages

Sometimes, it's beneficial to send output both to the monitor and to a file for logging. Instead of having to redirect output twice, you can use the special `tee` command.

The `tee` command is like a T-connector for pipes. It sends data from STDIN to two destinations at the same time. One destination is STDOUT . The other destination is a filename specified on the `tee` command line:

```
```
tee filename
```
```

Because `tee` redirects data from STDIN , you can use it with the pipe command to redirect output from any command:

```
```
$ date | tee testfile
Sun Jun 21 18:56:21 EDT 2020
```
```