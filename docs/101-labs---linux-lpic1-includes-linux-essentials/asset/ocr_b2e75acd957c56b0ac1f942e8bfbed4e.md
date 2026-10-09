# LAB 48

# Create, Monitor, and Kill Processes: Foreground and Background Jobs

**Lab Objective:**
Learn how to run jobs in the foreground and background.

**Lab Purpose:**
Sometimes, you want to run a process in Linux and then walk away, or hide the job in the background so you don't see it. In this lab, you will learn how to do that.

**Lab Tool:**
Ubuntu 18.04 (or another distro of your choice)

**Lab Topology:**
A single Linux machine, or virtual machine

**Lab Walkthrough:**

*Task 1:*

Open the Terminal and run `sleep 10000`, then press Ctrl+Z. Now run:

+   * jobs
+   * bg
+   * jobs
+   * fg

Hit Ctrl+C to cancel the sleep job.

When you first ran the `sleep` command and then pressed Ctrl+Z, that command was *stopped* (although the term “stopped” may be misleading—“paused” is more accurate). When stopped, a job is no longer running, ticking down seconds, or whatever it’s supposed to be doing. The `bg` command changes that, making the job run in the background. You can see the list of running jobs with `jobs`, and bring the most recent background job into the foreground with `fg`. Note that you can run `fg` on stopped jobs as well; you don't have to start them running first.