# xargs: Tandem Execution for "Not-So-Smart" Commands

We mentioned in the introduction to this section that there are two uses for xargs. Our first discussion and example illustrated how xargs can work with files that are smart enough to take input from a pipe. But unfortunately, not all commands are that smart. For example, rm (the delete command) is one of those not-so-smart commands. Faced with this situation, what would you do if you had a lot of repetitions of a command (such as rm) to perform? Your options are as follows:

+   Invoke the command several times manually.
+   Use some type of automated loop to invoke the command for every file, which spawns a subprocess every time the command is invoked (taxing on time and processing capability).
+   In the case of rm, use find to identify the input filenames and then execute cat, xargs, and rm in tandem.

The third option is the best. This example illustrates xargs’s second and very valuable use: taking cat’s output and passing it to rm. We will see how this process works in Example 9.2.

# Example 9.2 xargs

Juana’s portion of the RFI directory structure is illustrated in Figure 9.2. Juana now wants to remove the copies of RFI_Tel1, RFI_Tel2, and RFI_Tel3 that she has kept in her /home/gutieja/tempwork subdirectory. For the first part of the process, she will collect their filenames into a single file called temphone-lists. Then, she will cat that file to be sure that it is correct:

```
$ cd <Enter>
$ cd ~/tempwork<Enter>
$ find . -name '*Tel*' -print > ./temphone-lists<Enter>
$ cat temphone-lists<Enter>
./RFI_Tel1
./RFI_Tel2
./RFI_Tel3
```

Now, in the second and final stage, Juana will use xargs and rm against temphone-lists to remove the copies of the phone list files: