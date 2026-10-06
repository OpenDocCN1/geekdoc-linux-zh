
```bash
$ date >whoson
$ cat whoson
Thu Mar 27 14:31:18 PST 2003
$ who >>whoson
$ cat whoson
Thu Mar 27 14:31:18 PST 2003
root     console    Mar 27 05:00(::0)
alex      pts/4       Mar 27 12:23(::0)
alex      pts/5       Mar 27 12:33(::0)
jenny    pts/7       Mar 26 08:45 (bravo.tcorp.com)
```

Figure 5-11 Redirecting and appending output

## Pipes

The shell uses a pipe to connect standard output of one command directly to standard input of another command. A pipe (sometimes referred to as a pipeline) has the same effect as redirecting standard output of one command to a file and using that file as standard input to another command. A pipe does away with separate commands and the intermediate file. The symbol for a pipe is a vertical bar (|). The syntax of a command line using a pipe is

```bash
command_a [arguments] | command_b [arguments]
```

This command line uses a pipe to generate the same result as the group of command lines:

```bash
command_a [arguments] > temp
command_b [arguments] < temp
trm temp
```

In the preceding sequence of commands, the first line redirects standard output from command_a to an intermediate file named temp. The second line redirects standard input for command_b to come from temp. The final line deletes temp. The command using a pipe is not only easier to type, it is generally more efficient because it does not create a temporary file.

You can use a pipe with a member of the class of GNU/Linux utilities that accept either from a file specified on the command line or from standard input. You can also use pipes with commands that accept only input from standard input. For example, the tr (translate) utility (page 1362 in Part III) takes its input from standard input. In its simplest tr has the following format:

```bash
tr string1 string2
```

```bash
$ ls > temp
$ lpr temp
$ rm temp

or
$ ls | lpr
$
```

## Figure 5-12 A pipe

The tr utility accepts input from standard input and looks for characters that match one of the characters in string1. Finding a match, tr translates the character in string1 to the corresponding character in string2. (The first character in string1 translates into the first character in string2, and so forth.) In the following examples tr displays the contents of the abstract file with the letters a, b, and c-translated into A, B, and C, respectively:

```bash
$ cat abstract | tr abc ABC
```

```bash
$ tr abc ABC < abstract
```

The tr does not change the contents of the original file.
The lpr (line printer) utility is among the utilities that accept input from either a file or standard input. When you type the name of a file lpr on the command line, it places the file in the print queue. When you do not specify a filename on the command line, lpr takes input from standard input. This feature enables us to use a pipe to redirect input to lpr. The first set of commands in Figure 5-12 shows how you can use ls and lpr, with an intermediate file (temp), to send a list of files in the working directory to the printer. If the temp file exists, the first command overwrites its contents. The second set of commands sends the same list (with the exception of temp) to the printer, using a pipe.

The commands in Figure 5-13 redirect the output from the who utility to temp and then display this file in sorted order. The sort utility (page 66) takes its input

| who > temp |
| $ sort < temp |
| alex pts/4 Mar 27 12:23 |
| alex pts/5 Mar 27 12:33 |
| jenny pts/7 Mar 26 08:45 |
| root console Mar 27 05:00 |

## Figure 5-13 Using a temporary file to store intermediate results

```bash
$ who | sort
alex pts/4 Mar 27 12:23
alex pts/5 Mar 27 12:33
jenny pts/7 Mar 27 08:45
root console Mar 27 05:00
```

**Figure 5-14** A pipe doing the work of a temporary file

from the file specified on the command line, or when a file is not specified, a command line from standard input and sends its output to standard output. The sort command line in Figure 5-13 takes its input from standard input, which is redirected (<) to come from temp. The output that sort sends to the screen lists the users-in sorted (alphabetical order).

Because sort can take its input from standard input or from a filename you can omit the < symbol from Figure 5-13 to yield the same results.

Figure 5-14 achieves the same result without creating the temp file. Using a pipe, the shell redirects the output from `who` to the input of sort. The sort utility takes input from standard input because no filename follows it on the command line.

When a lot of people are using the system and you want information about only one of them, you can send the output from `who` to `grep`:

```bash
$ who | grep 'root'
root console Mar 27 05:00
```

Another way of handling output that is too long to fit on screen, such as a list of files, is to use `less`:

```bash
$ ls | less
```

## Filters

A filter is a program that processes input stream to produce output stream. The shell uses a pipe to connect standard output of one command directly to standard input of another command. A pipe (sometimes referred to as a pipeline) has the same effect as redirecting standard output of one command to a file and using that file as standard input to another command. A pipe does away with separate commands and the intermediate file. The symbol for a pipe is a vertical bar (|). The syntax of a command line using a pipe is

```bash
command_a [arguments] | command_b [arguments]
```

This command line uses a pipe to generate the same result as the group of command lines:

... (repeated text logic)

Because sort can take its input from standard input or from a filename you can omit the < symbol from Figure 5-13 to yield the same results. 

Figure 5-14 achieves the same result without creating the temp file. Using a pipe, the shell redirects the output from `who` to the input of sort. The sort utility takes input from standard input because no filename follows it on the command line.

When a lot of people are using the system and you want information about only one of them, you can send the output from `who` to `grep`:

```bash
$ who | grep 'root'
root console Mar 27 05:00
```

Another way of handling output that is too long to fit on screen, such as a list of files, is to use `less`:

```bash
$ ls | less
```
