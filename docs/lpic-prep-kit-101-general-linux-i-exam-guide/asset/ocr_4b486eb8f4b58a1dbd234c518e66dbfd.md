+   5. After entering the command in question 4, [3] 3321 appears on your display. What does it mean?
+   
+       a. The job number is 3 and the *PID* of the first process is 3321.
+       b. The job number is 3 and the *PID* of the last process is 3321.
+       c. The job contains 3 processes and the job number is 3321.
+       d. The job number is 3 and the *PID* of the parent process is 3321.

Answer a is incorrect; the *PID* is not that of the first process. **Answer b is correct; the job number is 3 and the PID (3321) is that of the last process.** Answer c is incorrect; the shell does not report the number of processes contained in the job. Answer d is incorrect; the shell does not report the *PID* of the parent process.

+   6. You want to type a very long string of commands on one command line; however, the line is longer than the display. How can you continue typing on another line without the operating system sending the enter to the shell?
+   
+       a. `commands/<Esc>more_commands`
+       b. `commands/<Esc>more_commands`
+       c. `commands/<Enter>more_commands`
+       d. `commands/<Enter>more_commands`

Answer a is incorrect; the `Esc` key does not enable you to wrap the lines. Answer b is incorrect; combining the `/` and `Esc` keys will not enable you to wrap the lines. Answer c is incorrect; the `Enter` key would be interpreted by the operating system as indicating the end of the command line and everything would be sent to the shell for processing. **Answer d is correct; the `/` tells the operating system to ignore the next key so that when passing your commands to the shell, the operating system would ignore the newline character.**

+   7. You type `PS1='\H \w]>` at the command line. What would this affect?
+   
+       a. Your prompt would be `[host_home,com hadde]>.``$`.
+       b. Your prompt would be `[host \home/hadden]>`.
+       c. Your prompt would be `[host_home.com hadde]>.``$`.
+       d. Your prompt would be `[host_home.com \home/hadden]>.``>`.

Answer a is incorrect; `\w` prints the `pwd` and the `$` should be >. Answer b is incorrect; `\H` prints the entire hostname. Answer c is incorrect; `\w` shows the `pwd`. **Answer d is correct; `\H` returns the full hostname, `\w` returns the `pwd`, and the `>` is defined for the end.**