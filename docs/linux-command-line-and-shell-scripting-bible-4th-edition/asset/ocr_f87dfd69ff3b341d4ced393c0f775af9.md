The period entry defines how often the jobs should be run, specified in days. The anacron program uses this entry to check against the jobs' time stamp file. The delay entry specifies how many minutes after the system starts the anacron program should run missed scripts.

# # NOTE

> **The anacron utility does not run scripts located in the /etc/cron.hourly directory. This is because the anacron program does not deal with scripts that have execution time needs of less than daily.**

The identifier entry is a unique non-blank character string — for example, cron_weekly . It is used to uniquely identify the job in log messages and error emails. The command entry contains the run-parts program and a cron script directory name. The run-parts program is responsible for running any script in the directory passed to it.

The at , cron , and anacron utilities all have their place in keeping your scripts running at their scheduled times. However, you may want a script's execution triggered when a user starts a new Bash shell instead of at a particular time on the clock. We'll look at that next.

# ## Starting scripts with a new shell

The ability to run a script every time a user starts a new Bash shell (even just when a specific user starts a Bash shell) can come in handy. Sometimes, you want to set shell features for a shell session or ensure that a specific file has been set.

Recall that the user's startup files run when they log into the Bash shell (covered in detail in Chapter 6, “Using Linux Environment Variables”). Also, remember that not every distribution has all the startup files. Essentially, the first file found in the following ordered list is run and the rest are ignored:

+   - $HOME/.bash_profile
+   - $HOME/.bash_login