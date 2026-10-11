Table 8.2. **sort Options and What They Do**

| Option | Action |
| :--- | :--- |
| -c | Checks to see that the file is sorted correctly |
| -d | Ignores all non-alphanumeric characters |
| -f | Considers all lowercase characters as uppercase |
| -i | Ignores non-printing characters |
| -m | Merges listed files |
| -r | Performs a reverse sort |


If you use `-c` with `sort`, it checks to see only whether the file is already sorted. If it is not, an error message is returned and `sort` exits. When using the `-m` with `sort`, the files to be merged must first be individually sorted.

`sort` does not change the original file. The results of using `sort` either go to the standard output or are saved to a file you designate. You can use `-o` with `sort` to designate the file to be used for the out file. This enables you to sort a file and save it to the same name.

# cut

The `cut` utility selects characters from the input and sends them to the standard output. It can be used to select tab delimited fields, too. Each character or field is referred to by the number of its position.

If the output of the `ls -l` command is

```
```
drwxrwxr-x    2 root     root       1024 Sep   9  07:41  graphics
-rw-R--r--     2 root     root       58575 May  20  13:40  install.txt
drwx------     2 haddenn  haddenn    1024 May   1  04:36  mail
-rw-r------     1 haddenn  haddenn    1633 May  16  09:07  mbox
-rw-rw-r--      1 haddenn  haddenn       40 May  20  22:22  mywords
drwx------     2 haddenn  haddenn    1024 May   8  15:18  nemail
-rw-rw-r--      0 Sep    4  16:53  script
drwxr-xF-x     2 haddenn  haddenn    1024 May   7  20:55  temp
```
```

and if you wanted to see only characters 2\[nd\]10 (permissions), you could issue the following command:

```
ls -1 | cut -c2-10
```
The `-c` option lists the characters to be displayed, and the `|` (pipe) tells `cut` to get its input from the `ls -1` command. The output would be

```
rwxrwxr-x
rw-r-r--
```