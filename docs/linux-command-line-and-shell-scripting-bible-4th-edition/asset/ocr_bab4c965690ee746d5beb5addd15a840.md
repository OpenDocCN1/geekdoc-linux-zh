| Column | Description |
| :--- | :--- |
| COMMAND | The first nine characters of the name of the command in the process |
| PID | The process ID of the process |
| USER | The login name of the user who owns the process |
| FD | The file descriptor number and access type (r – [read], w – [write], u – [read/write]) |
| TYPE | The type of file (CHR – [character], BLK – [block], DIR – [directory], REG – [regular file]) |
| DEVICE | The device numbers (major and minor) of the device |
| SIZE | If available, the size of the file |
| NODE | The node number of the local file |
| NAME | The name of the file |

The file type associated with **STDIN**, **STDOUT**, and **STDERR** is character mode. Because the **STDIN**, **STDOUT**, and **STDERR** file descriptors all point to the terminal, the name of the output file is the device name of the terminal. All three standard files are available for both reading and writing (although it does seem odd to be able to write to **STDIN** and read from **STDOUT**).

Now, let’s look at the results of the lsof command from inside a script that’s opened a couple of alternative file descriptors:

```
$ cat test18
#!/bin/bash
# testing lsof with file descriptors

exec 3> test18file1
exec 6> test18file2
exec 7> testfile

/usr/sbin/lsof -a -p $$ -d0,1,2,3,6,7
$ ./test18
COMMAND PID USER    FD TYPE DEVICE SIZE     NODE NAME
test18  3594 rich   0u  CHR  136,0          2 /dev/pts/0
test18  3594 rich   1u  CHR  136,0          2 /dev/pts/0
test18  3594 rich   2u  CHR  136,0          2 /dev/pts/0
18  3594 rich     3w  REG  253,0   0 360712
```