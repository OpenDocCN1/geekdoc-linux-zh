arrow (>) switch. You cannot redirect with a double left arrow (<<); therefore, answer a is incorrect. Because stdout cannot be redirected with the error redirect arrow (2>), answer b is incorrect. If you're redirecting standard error (stderr), you need to use 2>>, and not the double right arrow (>>). Therefore, answer c is incorrect.

# Question 7

A user wants to open a text file from an MS-DOS directory named big memo.txt. Whenever he tries to open the file, he sees the following message:

```
big: No such file or directory
```

This user needs your help. Which of the following commands do you tell this user to run? This file is part of the /disks/c/data directory.

+   - a. vi /disks/c/data/big memo.txt
+   - b. vi /disks/c/data/big\ memo.txt
+   - c. vi /disks/c/data/big/ memo.txt /
+   - d. vi /disks/c/data/bigmemo.txt

Answer b is correct. The backslash (\ ) keeps the shell from interpreting characters such as the question mark (?), asterisk (*), and space. The backslash in answer b allows the vi editor to see these characters for what they are, instead of interpreting them as wildcards or new files. Because there is no backslash that "escapes" the space in answers a and c, these answers are both incorrect. Because there is no space after the backslash, answer d opens the bigmemo.txt file; therefore, this answer is incorrect.