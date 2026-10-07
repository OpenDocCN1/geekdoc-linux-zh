# Chapter 11: I/O and TRAP Processing 499

If you are supplying a prompt string and using multiple input buffers, as in the present example, the prompt string must follow the first input buffer name.

![](bbox=[0.025, 0.093, 0.125, 0.163])

You can use the default input buffer, REPLY, and also have a prompt string by naming REPLY explicitly, as in the following command:

```
read REPLY?"Your input: 
```

![](bbox=[0.025, 0.187, 0.125, 0.257])

+   e) How does the output of these two commands compare?

Answer:Your interaction should look like the following:

```
[11006]: wc < wctest
3 12 56
[11007]: mywc < wctest
3 12 53
```

Both commands print out there three similar numbers, but they are not identical, and their spacing is different. The reasons for the differences can be attributed to the difference between how the shell's read command operates compared with the logic of the C language code that was used to generate the wc command. The matter of how the numbers are spaced is not important here, but the fact that the final numbers output by the two programs are different is significant: The new line characters (the ASCII "linefeed" code) at the end of each line are removed by the read command, but the system's wc reads and counts them the same as any other characters in the file. If you used a non-UNIX editor to prepare your data file, there would be both an ASCII "carriage return" code, as well as a new line at the end of each line, and your results would differ accordingly (The values would be 59 and 56, instead of 56 and 53).

+   f Does the shell do field splitting when the read at the top of the loop is executed?

Answer: No, because IFS is the empty string whenever this read command is executed.

The empty string is assigned to IFS before the while loop is entered the first time, then again as the last statement of the loop, returning to the top to execute read again.