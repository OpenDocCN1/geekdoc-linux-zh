# Q The printer is very slow. How can I speed it up?

A You might be able to fix this problem by setting the printer to polled mode with the `lptcontrol` program. This can be done with the command `lptcontrol -P`. Don't forget that you need to add this to a startup file if you want it to take effect on each system boot.

# Quiz

+   1. The file that contains printer definitions is
+      A. `/etc/printers`
+      B. `/etc/print.conf`
+      C. `/etc/printcap`
+      D. `/etc/printdef`
+   
+   2. One printer should always be aliased to which of the following?
+      A. `lpc`
+      B. `lpd`
+      C. `lpr`
+      D. `lp`
+   
+   3. Which of the following programs can be used to look at printer queues?
+      A. `lpd`
+      B. `lpr`
+      C. `lpc`
+      D. `lpq`
+   
+   4. Which of the following commands controls printers and their queues?
+      A. `lpd`
+      B. `lpc`
+      C. `lptcontrol`
+      D. None of the above
+   
+   5. Which of the following commands removes a job from the queue?
+      A. `lprremove`
+      B. `lpr`
+      C. `lprm`
+      D. `lpdelete`

![](bbox=[0.88, 0.32, 0.98, 0.48])