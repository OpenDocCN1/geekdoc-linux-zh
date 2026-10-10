# Answers to Guided Exercises

+   1. In addition to text files, the command `cat` can also work with binary data, like sending the contents of a block device to a file. Using redirection, how can `cat` send the contents of device `/dev/sdc` to the file `sdc.img` in the current directory?

```
`$ cat /dev/sdc > sdc.img`
```

+   2. What’s the name of the standard channel redirected by the command `date 1> now.txt`?

Standard output or `stdout`

+   3. After trying to overwrite a file using redirection, a user gets an error informing that the option `noclobber` is enabled. How can the option `noclobber` be deactivated for the current session?

```
`set +C` or `set +o noclobber`
```

+   4. What will be the result of command `cat <</dev/stdout`?

Bash will enter Heredoc input mode, then exit when a period appears in a line by itself. The typed text will be redirected to `stdout` (printed on screen).