# **Relevant Fedora Commands**

Here are some of the commands you learned so far:

+   > **chkconfig**—Fedora's text-only command-line runlevel configuration utility
+   
+   > **ntsysv**—Fedora's text-based system services configuration tool for the
+   > command line
+   
+   > **setup**—Actually a bash script, it is a menu to all the individual ncurses-based
+   > configuration tools, including `ntsysv`
+   
+   > **system-config-services**—Fedora's GUI runlevel configuration tool, named
+   > Configure Services
+   
+   > **telinit**—Changes the current runlevel

# **Scheduling Tasks**

There are three ways to schedule commands in Fedora, all of which work in different
ways. The first is the `at` command, which specifies a command to run at a specific time
and date relative to today. The second is the `batch` command, which is actually a script
that redirects you to the `at` command with some extra options set so that your command
runs when the system is quiet. The last option is the `cron` daemon, which is the Linux
way of executing tasks at a given time.

# **Using at and batch to Schedule Tasks for Later**

If there is a time-intensive task you want to run, but you do not want to do it while you
are still logged in, you can tell Fedora to run it later with the `at` command. To use at, you
need to tell it the time at which you want to run and then press Enter. You then see a
new prompt that starts with `at>`, and everything you type there—until you press Ctrl+D—
comprises the commands you want at to run.

When the designated time arrives, at performs each action individually and in order,
which means later commands can rely on the results of earlier commands. In this next
example, run at just after 5 p.m., at is used to download and extract the latest Linux
kernel at a time when the network should be quiet:

```
[paul@caitlin ~]$ at now + 7 hours
at> wget http://www.kernel.org/pub/linux/kernel/v2.6/linux-2.6.10.tar.bz2
at> tar xvfj linux-2.6.10.tar.bz2
at> <EOT>
job 2 at 2005-01-09 17:01
```

Specifying `now + 7 hours` as the time does what you would expect: at was run at 5 p.m.,
so the command runs just after midnight that night. When your job finishes, at sends
you mail with a full log of your job's output; type `mail` at the console to bring up your
mailbox and then press the relevant number to read at's mail.