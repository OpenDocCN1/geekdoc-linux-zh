```
$ echo "demonstration of prompt string
> 2"
demonstration of prompt string
2
$ PS2="secondary prompt: "$ echo "this demonstrates
secondary prompt: prompt string 2"
this demonstrates
prompt string 2
```

The second command changes the secondary prompt to `secondary prompt:` followed by a SPACE. A multiline `echo` demonstrates the new prompt.

# PS3: Menu Prompt

The PS3 variable holds the menu prompt for the `select` control structure (page 984).

# PS4: Debugging Prompt

The PS4 variable holds the `bash` debugging symbol (page 966).

# IFS: Separates Input Fields (Word Splitting)

The `IFS` (Internal Field Separator) shell variable specifies the characters you can use to separate arguments on a command line. It has the default value of `SPACE TAB NEWLINE`. Regardless of the value of `IFS`, you can always use one or more SPACE or TAB characters to separate arguments on the command line, provided these characters are not quoted or escaped. When you assign `IFS` character values, these characters can also separate fields—but only if they undergo expansion. This type of interpretation of the command line is called *word splitting*.

**Be careful when changing IFS**

caution Changing `IFS` has a variety of side effects, so work cautiously. You may find it useful to save the value of `IFS` before changing it. Then you can easily restore the original value if you get unexpected results. Alternatively, you can fork a new shell with a **bash** command before experimenting with `IFS`; if you get into trouble, you can **exit** back to the old shell, where `IFS` is working properly.

The following example demonstrates how setting `IFS` can affect the interpretation of a command line:

```
$ a=w:x:y:z

$ cat $a
cat: w:x:y:z: No such file or directory
$ IFS=";"

$ cat $a
cat: w: No such file or directory
cat: x: No such file or directory
cat: y: No such file or directory
cat: z: No such file or directory
```