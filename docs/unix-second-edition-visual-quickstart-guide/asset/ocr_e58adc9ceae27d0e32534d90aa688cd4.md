# Running Jobs in the Background with bg

If you're running a job that doesn't require input from you, consider running it in the background using bg (Code Listing 9.7). In doing so, you can keep the program running while working on other Unix activities at the same time.

# To run jobs in the background with bg:

+   1. `jobs`
+   
+      At the shell prompt, type `jobs` to see the list of all jobs, running or stopped. Note the job numbers on the left.
+   
+   2. `bg %1`
+   
+      Type `bg` followed by `%` and the number of the job you want to run in the background (Code Listing 9.7).

# ✔ Tips

+   ▪ If you want to put the most recently suspended job into the background, just type `bg` (without the number) at the prompt.
+   
+   ▪ You can also put jobs directly into the background without first suspending them. Just type the name of the job to run, a space, and `&` (as in `bigdog &`). The `&` moves the job directly into the background.

```
[ejr@hobbes ejr]$ jobs
[1]-  Stopped (tty input) ftp
[2]+  Stopped (tty input) telnet
[3]   Stopped (signal) lynx
[4]+  Stopped  man telnet
[ejr@hobbes ejr]$ bg %1
[1]-  ftp calvin.raycomm.com &
[ejr@hobbes ejr]$
```

**Code Listing 9.7** Restarting suspended jobs in the background lets you do two things—or more—at once. To move a job to the background, just type `bg` followed by `%` and the job number.