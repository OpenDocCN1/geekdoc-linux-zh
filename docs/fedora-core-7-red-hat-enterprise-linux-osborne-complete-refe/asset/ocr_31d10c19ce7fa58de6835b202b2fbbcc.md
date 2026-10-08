standard output. However, the standard input has been redirected to receive its data from a file, while the standard output has been redirected to place its data in a file.

```
$ cat < mletter > newletter
```

# Pipes: |

You may find yourself in situations in which you need to send data from one command to another. In other words, you may want to send the standard output of a command to another command, not to a destination file. Suppose you want to send a list of your filenames to the printer to be printed. You need two commands to do this: the `ls` command to generate a list of filenames and the `lpr` command to send the list to the printer. In effect, you need to take the output of the `ls` command and use it as input for the `lpr` command. You can think of the data as flowing from one command to another. To form such a connection in Linux, you use what is called a *pipe*. The *pipe operator* (`|`, the vertical bar character) placed between two commands forms a connection between them. The standard output of one command becomes the standard input for the other. The pipe operation receives output from the command placed before the pipe and sends this data as input to the command placed after the pipe. As shown in the next example, you can connect the `ls` command and the `lpr` command with a pipe. The list of filenames output by the `ls` command is piped into the `lpr` command.

```
$ ls | lpr
```

You can combine the `pipe` operation with other shell features, such as file expansion characters, to perform specialized operations. The next example prints only files with a .c extension. The `ls` command is used with the asterisk and “`.c`” to generate a list of filenames with the .c extension. Then this list is piped to the `lpr` command.

```
$ ls *.c | lpr
```

In the preceding example, a list of filenames was used as input, but what is important to note is that pipes operate on the standard output of a command, whatever that might be. The contents of whole files or even several files can be piped from one command to another. In the next example, the `cat` command reads and outputs the contents of the mydata file, which are then piped to the `lpr` command:

```
$ cat mydata | lpr
```

Linux has many commands that generate modified output. For example, the `sort` command takes the contents of a file and generates a version with each line sorted in alphabetic order. The `sort` command works best with files that are lists of items. Commands such as `sort` that output a modified version of its input are referred to as *filters*. Filters are often used with pipes. In the next example, a sorted version of mylist is generated and piped into the `more` command for display on the screen. Note that the original file, mylist, has not been changed and is not itself sorted. Only the output of `sort` in the standard output is sorted.

```
$ sort mylist | more
```