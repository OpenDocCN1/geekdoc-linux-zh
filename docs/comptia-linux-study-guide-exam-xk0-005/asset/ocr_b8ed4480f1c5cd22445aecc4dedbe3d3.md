# **TABLE 4.7** Commonly used redirection operators

| Operator | Description |
| :--- | :--- |
| > | Redirect STDOUT to specified file. If file exists, overwrite it. If it does not exist, create it. |
| >> | Redirect STDOUT to specified file. If file exists, append to it. If it does not exist, create it. |
| 2> | Redirect STDERR to specified file. If file exists, overwrite it. If it does not exist, create it. |
| 2>> | Redirect STDERR to specified file. If file exists, append to it. If it does not exist, create it. |
| &> | Redirect STDOUT and STDERR to specified file. If file exists, overwrite it. If it does not exist, create it. |
| &>> | Redirect STDOUT and STDERR to specified file. If file exists, append to it. If it does not exist, create it. |
| < | Redirect STDIN from specified file into command. |
| <> | Redirect STDIN from specified file into command and redirect STDOUT to specified file. |

In Listing 4.19, the pr utility displays the two files numbers.txt and random.txt side by side. You can see that differences exist between these two files. A new copy of the numbers.txt file is created, so any changes are only made to the new file, n.txt, in case anything goes wrong. The diff command uses the -e switch to create an ed script. This script will make the n.txt file the same as the random.txt file.

Prior to enacting the created script, a few additional items must be added to it. In Listing 4.20, the echo command is used two times to append letters to the script.

```
**Listing 4.20:** Update an ed script via redirection operators

```
$ echo w >> switch.sh
$ echo q >> switch.sh
$
$ cat switch.sh
5c
0000 0010
```

```