In this example, I used the cat command to view the tux user's crontab file. However, you can also use the crontab -l command to display your user's crontab file. You can also use the crontab -r command to remove your user's crontab file. Let's practice working with Linux processes in the following exercise.

# Exercise 13-2: Scheduling Linux Processes

![](bbox=[0.05, 0.22, 0.61, 0.27])

In this exercise, you will practice using cron and at commands to schedule processes to run in the future on your system. Complete the following:

+   1.  Boot your Linux system and log in as a standard user.
+   2.  Open a terminal session.
+   3.  Switch to your root user account by entering su - followed by your root user's password.
+   4.  Practice using the at daemon by doing the following:
+       a. At the shell prompt, enter **atd** *status*.
+       b. Verify that the *at* daemon is running. If it isn't, enter **atd** *start* at the shell prompt.
+       c. At the shell prompt, enter **now** *+ 5 minutes*.
+       d. At the *at* prompt, enter `ps -ef > ~/psoutput.txt`.
+       e. Press <kbd>CTRL</kbd>-D.
+       f. Generate a listing of pending *at* jobs by entering **atq**. You should see the job you just created.
+       g. Wait for the pending *at* job to complete.
+       h. Check the ~/psoutput.txt file and verify that the output from the *ps* command was generated correctly.
+       i. At the shell prompt, enter `2pm tomorrow`.
+       j. At the *at* prompt, enter `ps -ef > ~/psoutput.txt`.
+       k. Press ENTER.
+       l. Press <kbd>CTRL</kbd>-D.
+       m. Generate a listing of pending *at* jobs by entering **atq**. You should see the job you just created. Note its job number.
+       n. Remove the pending job by entering **atrm** *job_number*.
+       o. Enter **atq** again. The pending job should be gone.
+   5.  Practice using *cron* by completing the following:
+       a. Log out of your root user account by entering **exit**.