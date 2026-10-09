# ACTIVITY 1-6

# Starting and Stopping Linux

**Before You Begin:**
You have logged in as *root* in the CLI.

**Scenario:**
You are given the task of managing the implementation of Linux at your company. To begin, you must learn to start and stop your Linux system and familiarize yourself with various runlevels.

| What You Do | How You Do It |
| --- | --- |
| 1. Examine various runlevels. | a. At the command line, enter `more /etc/inittab` |
|  | b. Press the Spacebar two times to continue. |
|  | c. Observe the contents of the `/etc/inittab` file displayed on the monitor. |
|  | d. Enter `runlevel` to determine your current runlevel. |
|  | e. Observe your current runlevel. |
| 2. Switch to the single-user mode. | a. At the command line, enter `telinit 1` |
|  | b. Observe that the services of previous runlevel are stopped and runlevel 1 service has started. |
|  | c. Enter `runlevel` to verify that you are in single-user mode. |
|  | d. Observe that the command shows `1 S`, for single user `1`. |
|  | e. Enter `exit` to return to the default runlevel, which is runlevel 5. |
|  | f. Press Ctrl+Alt+F1 to switch to the first terminal of the CLI. |
|  | g. At the login prompt, enter `root` |
|  | h. At the password prompt, enter `p@ssw0rd` |