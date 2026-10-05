![](bbox=[0.435, 0.087, 0.658, 0.287])

# Figure 7-9 Redirecting standard input

Figure 7-10 shows cat with input redirected from the supply_orders file created in Figure 7-8 and standard output going to the screen. This setup causes cat to display the sample file on the screen. The system automatically supplies an EOF signal at the end of an ordinary file.

Utilities that take input from a file or standard input Giving a cat with input redirected from a file yields the same result as giving a cat command with the filename as an argument. The cat utility is a member of class of Linux utilities that function in this manner. Other members of this class include ip, sort, grep, and Perl. These utilities first examine the command line that you call them. If you include a filename on the command line, the utility takes its input from the file you specify. If you do not specify a filename, the utility takes its input from standard input. It is the utility or program—not the shell or operating system—that functions in this manner

# noclober: AVOIDS OVERWRITING FILES

The shell provides the noclober feature that prevents overwriting a file using redirection. Enable this feature by setting noclober using the command -o noclober. The same command with +o sets noclober. With noclober set, if you redirect to an existing file, the shell displays an error message and does not execute the command. The following example creates a file using touch, sets noclober, and attempts to redirect the output from echo to the newly created file, uses noclober, and performs the redirection

```
$ touch tmp
$ -o noclober
$ echo "hi there" > tmp
bash tmp: cannot overwrite existing file
$ +o noclober
$ echo "hi there" > tmp
```

You can override noclober by putting a pipe symbol after the redirect symbol (>). In the following example, the user creates a file by redirecting the output of date.