which error messages appear on the console, which are sent as email, and which go to one of several log files.

System administrators are frequently called upon to set up and administrate MySQL databases. MySQL is the M in LAMP (Linux, Apache, MySQL, PHP/Perl/Python), an open-source enterprise software stack. Many programming languages provide an interface to MySQL (e.g., C, PHP, Perl).

# ## EXERCISES

+   1. How would you list all the processes running vi?

+   2. How would you use kill to cause a server process to reread its configuration files?

+   3. From the command line, how would you create a user named John Doe who has the username jd and who belongs to group 65535?

+   4. How would you notify users that you are going to reboot the system in ten minutes?

+   5. Give a command that creates a level 0 dump of the /usr filesystem on the first tape device on the system. Which command would you use to take advantage of a drive that supports compression? Which command would place a level 3 dump of the /var filesystem immediately after the level 0 dump on the tape?

# ## ADVANCED EXERCISES

+   6. If the system is less responsive than normal, what is a good first step in figuring out where the problem is?

+   7. A process stores its PID number in a file named **process.pid**. Write a command line that terminates this process.

+   8. Working with root privileges, you are planning to delete some files but want to make sure that the wildcard expression you use is correct. Suggest two ways you could make sure you delete the correct files.

+   9. Create a crontab file that will regularly perform the following backups:
+   a. Perform a level 0 backup once per month.
+   b. Perform a level 2 dump one day per week.
+   c. Perform a level 5 dump every day on which neither a level 0 nor a level 2 dump is performed.
+   
+   In the worst-case scenario, how many restore commands would you have to give to recover a file that was dumped using this schedule?