A potential problem with piping the output of one command into the input of another is that some commands will only accept a certain amount of input at a time, and may complain if they have massive outputs thrown at them. The solution to this is the `xargs` command, which will accept the input stream and split it into chunks to pass along a bit at a time and repeatedly running the downstream command until the input stream ends. It is often used with `find` to run a command for each item found. The following example will move all of Bob's music files into his music directory:

```
find . -name "*.mp3" -u bob|xargs -i mv {} ./bobs_mp3s
```

There are other ways to string commands together, too. By putting a ";" between two commands, they will run consecutively – when the first one is finished, the second one will start:

```
do_this_first; then_do_this; and_finally_this
```

Note that spaces are ignored, and can be used before, after, both, or not at all.

> **Note**
> 
> Two interesting variations of the ; function are &&, which only runs the next command if the first one completes without an error, and || runs the next command only if the first one fails – handy for sending a message to notify someone of the problem.

The "=" is used to set a variable equal to a value using the format `name=value`, as shown in Figure 6.13.

![](bbox=[0.28, 0.7, 0.9, 0.95])

# FIGURE 6.13

An example of setting a variable equal to a value.