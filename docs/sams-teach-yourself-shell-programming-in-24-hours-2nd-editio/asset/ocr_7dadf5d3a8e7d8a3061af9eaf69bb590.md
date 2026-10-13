```
19      cp -r docs backup
20      Failed
21      [nh] [No] [00]
-> //buggy2.sh: syntax error at line 21: '}' unexpected
```

Based on this output, the problem is apparent: Line 20 does not terminate the first pattern of the case statement with ;;. You can make either of the following changes to fix the script:

```
Failed ;;

or

Failed
;;
```

After making either of these change, you find that the command

$ /bin/sh -n buggy2.sh

does not produce an error message. As you will see in the next section, this does not necessarily mean that the script is bug free.

# Shell Tracing

There are many instances when syntax checking will give your script a clean bill of health, even though bugs are still lurking within it. Running syntax checking on a shell script is similar to running a spelling checker on a text document—it might find most of the misspellings, but it can't fix problems like read spelled red. In order to find and fix these types of errors in a text document, you need to proofread it. Shell tracing is proofreading your shell script.

In shell tracing mode each command is printed in the exact form that it is executed. For this reason, shell tracing mode is often referred to as execution tracing mode. Shell tracing is enabled by the -x option (as in execution). The following command enables tracing for an entire script:

```
$ /bin/sh -x script arg1 arg2 ... argN
```

Tracing can also be enabled using the set command:

```
set -x
```