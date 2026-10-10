
which counts the number of characters. Strings containing spaces must be inside quotes, otherwise only the first word will be used as the Here string and the remaining ones will be passed as arguments to the command.

## Guided Exercises

- In addition to text files, the command `cat` can also work with binary data, like sending the contents of a block device to a file. Using redirection, how can `cat` send the contents of device `/dev/sdc` to the file `sdc.img` in the current directory?
- What's the name of the standard channel redirected by the command `date 1> now.txt`?
- After trying to overwrite a file using redirection, a user gets an error informing that option `noclobber` is enabled. How can the option `noclobber` be deactivated for the current session?
- What will be the result of command `cat <</dev/stdout`?

## Explorational Exercises

- The command `cat /proc/cpu_info` displays an error message because `/proc/cpu_info` is nonexistent. The command `cat /proc/cpu_info 2>1` redirects the error message to where?
- Will it still be possible to discard content sent to `/dev/null` if the `noclobber` option is enabled for the current shell session?
- Without using `echo`, how could the contents of the variable `$USER` be redirected to the stdin of command `sha1sum`?
- The Linux kernel keeps symbolic links in `/proc/PID/fd/` to every file opened by a process, where *PID* is the identification number of the corresponding process. How could the system administrator use that directory to verify the location of log files opened by *nginx*, supposing its PID is *1234*?
- It’s possible to do arithmetic calculations using only shell builtin commands, but floating point calculations require specific programs, like *bc* (*basic calculator*). With *bc* it’s even possible to specify the number of decimal places, with parameter `scale`. However, *bc* accepts operations only through its standard input, usually entered in interactive mode. Using a Here string, how can the floating point operation `scale=6; 1/3` be sent to the standard input of *bc*?

## Summary

This lesson covers methods to run a program redirecting its standard communication channels. Linux processes use these standard channels as generic *file descriptors* to read and to write data, making it possible to arbitrarily change them to files or devices. The lesson goes through the following steps:

- What file descriptors are and the role they play in Linux.
- The standard communication channels of every process: *stdin*, *stdout* and *stderr*.
- How to correctly execute a command using data redirection, both for input and output.
- How to use *Here Documents* and *Here Strings* in input redirections.

The commands and procedures addressed were:

- Redirection operators: `>`, `<`, `>>`, `<<`, `<<<`.
- Commands `cat`, `set`, `uniq` and `wc`.

## Answers to Guided Exercises

- In addition to text files, the command `cat` can also work with binary data, like sending the contents of a block device to a file. Using redirection, how can `cat` send the contents of device `/dev/sdc` to the file `sdc.img` in the current directory?

```bash
$ cat /dev/sdc > sdc.img
```

- What’s the name of the standard channel redirected by the command `date 1> now.txt`?

Standard output or `stdout`

- After trying to overwrite a file using redirection, a user gets an error informing that the option `noclobber` is enabled. How can the option `noclobber` be deactivated for the current session?

```bash
set +C
# or
set +o noclobber
```

- What will be the result of command `cat <</dev/stdout`?

Bash will enter Heredoc input mode, then exit when a period appears in a line by itself. The typed text will be redirected to `stdout` (printed on screen).

## Answers to Explorational Exercises

- The command `cat /proc/cpu_info` displays an error message because `/proc/cpu_info` is nonexistent. The command `cat /proc/cpu_info 2>1` redirects the error message to where?

To a file named 1 in the current directory.

- Will it still be possible to discard content sent to `/dev/null` if the `noclobber` option is enabled for the current shell session?

Yes. `/dev/null` is a special file not affected by `noclobber`.

- Without using `echo`, how can the contents of the variable `$USER` be redirected to the stdin of command `sha1sum`?

```bash
$ sha1sum <<<$USER
```

- The Linux kernel keeps symbolic links in `/proc/PID/fd/` to every file opened by a process, where `PID` is the identification number of the corresponding process. How could the system administrator use that directory to verify the location of log files opened by `nginx`, supposing its PID is `1234`?

By issuing the command `ls -l /proc/1234/fd/`, which will display the target of every symbolic link in the directory.

- It's possible to do arithmetic calculations using only shell builtin commands, but floating point calculations require specific programs, like `bc` (*basic calculator*). With `bc` it's even possible to specify the number of decimal places, with parameter `scale`. However, `bc` accepts operations only through its standard input, usually entered in interactive mode. Using a Here string, how could the floating point operation `scale=6; 1/3` be sent to the standard input of `bc`?

```bash
$ bc <<<"scale=6; 1/3"
```

![img/824749d5fc1d265354d0e66a01af9ced_287_0.png](img/824749d5fc1d265354d0e66a01af9ced_287_0.png)

## 103.4 Lesson 2

| **Certificate:** | LPIC-1 (101) |
| :--- | :--- |
| **Version:** | 5.0 |
| **Topic:** | 103 GNU and Unix Commands |
| **Objective:** | 103.4 Use streams, pipes and redirects |
| **Lesson:** | 2 of 2 |

### Introduction

One aspect of the Unix philosophy states that each program should have a specific purpose and should not try to incorporate features outside its scope. But keeping things simple does not mean less elaborated results, because different programs can be chained together to produce a combined output. The vertical bar character `|`, also known as the *pipe* symbol, can be used to create a pipeline connecting the output of a program directly into the input of another program, whereas *command substitution* allows to store the output of a program in a variable or use it directly as an argument to another command.

### Pipes

Unlike redirects, with pipes data flows from left to right in the command line and the target is another process, not a filesystem path, file descriptor or Here document. The pipe character `|` tells the shell to start all distinct commands at the same time and to connect the output of the previous command to the input of the following command, left to right. For example, instead of using redirects, the content of the file `/proc/cpuinfo` sent to the standard output by `cat` can be piped to the stdin of `wc` with the following command:

```bash
$ cat /proc/cpuinfo | wc
208   1184   6096
```

In the absence of a path to a file, wc counts the number of lines, words and characters it receives on its stdin, as is the case in the example. Many pipes can be present in a compound command. In the following example, two pipes are used:

```bash
$ cat /proc/cpuinfo | grep 'model name' | uniq
model name        : Intel(R) Xeon(R) CPU        X5355 @ 2.66GHz
```

The content of file `/proc/cpuinfo` produced by `cat /proc/cpuinfo` was piped to the command `grep 'model name'`, which then selects only the lines containing the term `model name`. The machine running the example has many CPUs, so there are repeated lines with `model name`. The last pipe connects `grep 'model name'` to `uniq`, which is responsible for skipping any line equal to the previous one.

Pipes can be combined with redirects in the same command line. The previous example can be rewritten to a simpler form:

```bash
$ grep 'model name' </proc/cpuinfo | uniq
model name        : Intel(R) Xeon(R) CPU        X5355 @ 2.66GHz
```

The input redirect for `grep` is not strictly necessary as `grep` accepts a file path as argument, but the example demonstrates how to build such combined commands.

Pipes and redirects are exclusive, that is, one source can be mapped to only one target. Yet, it is possible to redirect an output to a file and still see it on the screen with program `tee`. To do it, the first program sends its output to the stdin of `tee` and a file name is provided to the latter to store the data:

```bash
$ grep 'model name' </proc/cpuinfo | uniq | tee cpu_model.txt
model name        : Intel(R) Xeon(R) CPU        X5355 @ 2.66GHz
$ cat cpu_model.txt
model name        : Intel(R) Xeon(R) CPU        X5355 @ 2.66GHz
```

The output of the last program in the chain, generated by `uniq`, is displayed and stored in the file `cpu_model.txt`. To not overwrite the content of the provided file but to append data to it, the option `-a` must be provided to `tee`.
