```
```
command_a [arguments] > temp
command_b [arguments] < temp
rm temp
```
```

In the preceding sequence of commands, the first line redirects standard output from `command_a` to an intermediate file named `temp`. The second line redirects standard input for `command_b` to come from `temp`. The final line deletes `temp`. The pipeline syntax is not only easier to type but also is more efficient because it does not create a temporary file.

**optional** More precisely, a `bash` pipeline comprises one or more simple commands (page 147) separated by a `|` or `|&` control operator. A pipeline has the following syntax:

```
```
[time] [|] command1 [|||& command2 ... ]
```
```

where `time` is an optional utility that summarizes the system resources used by the pipeline, `!` logically negates the exit status returned by the pipeline, and the `commands` are simple commands (page 147) separated by `|` or `|&`. The `|` control operator sends standard output of `command1` to standard input of `command2`. The `|&` control operator is short for `2>&1 |` (see “Sending errors through a pipeline” on page 335) and sends standard output and standard error of `command1` to standard input of `command2`. The exit status of a pipeline is the exit status of the last simple command unless `pipefail` (page 403) is set, in which case the exit status is the rightmost simple command that failed (returned a nonzero exit status) or zero if all simple commands completed successfully.

# Examples of Pipelines

**10** `tr` You can include in a pipeline any utility that accepts input either from a file specified on the command line or from standard input. You can also include utilities that accept input only from standard input. For example, the `tr` (translate) utility takes its input from standard input only. In its simplest usage `tr` has the following syntax:

```
```
tr string1 string2
```
```

The `tr` utility accepts input from standard input and looks for characters that match one of the characters in `string1`. Upon finding a match, it translates the matched character in `string1` to the corresponding character in `string2`. That is, the first character in `string1` translates into the first character in `string2`, and so forth. The `tr` utility sends its output to standard output. In both of the following `tr` commands, `tr` displays the contents of the `abstract` file with the letters a, b, and c translated into A, B, and C, respectively:

```
```
$ cat abstract
I took a cab today!

$ cat abstract | tr abc ABC
I took A CAB today!
$ tr abc ABC < abstract
I took A CAB today!
```
```