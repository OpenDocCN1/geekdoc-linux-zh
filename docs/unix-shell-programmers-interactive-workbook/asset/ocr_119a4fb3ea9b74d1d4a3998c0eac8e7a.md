# Lab 2.3: Command Syntax

Control-C cancels (kills) a program, and Control-D indicates the end of input from a terminal. The cat command is programmed to stop when it comes to the end of its input (^D). Canceling a program is generally considered a heavy-handed way to get it to stop.

![](bbox=[0.135, 0.095, 0.205, 0.165])

You can use the stty command to change what characters you type to perform these operations.

+   a) What did you observe

+   b) What two devices are stdin and stdout connected to?

Redirect stdout so that cat copies what you type to a file named out. Do this twice, once with the redirection symbol and file name before the command name, and again with them after the command name.

+   c) What did you observe

Possible Problem! If you redirect stdout to a file that already exists, you may get an error message. Use the command set -o noclobobber to overcome this problem. You'll learn why this works in the next exercise.

![](bbox=[0.135, 0.695, 0.215, 0.765])

+   d) Does it matter whether you put the output redirection before or after the command name?