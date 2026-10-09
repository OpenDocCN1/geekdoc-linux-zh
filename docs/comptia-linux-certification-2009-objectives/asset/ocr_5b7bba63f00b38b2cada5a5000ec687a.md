# **ACTIVITY 11-4**
Analyzing Log Files

**Before You Begin:**
1. You have logged in as root in the GUI.
2. The terminal window is displayed.
3. Switch to the CLI.

**Scenario:**
Your manager asked you to analyze the log files and document the results. To do this, you need to:
* Monitor the usage of the root login to prevent unauthorized usage.
* Prepare a list of users with their login name, GID, and home directory.
* Generate a report with the group name and GID.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Locate the instances of root login usage. | a. Enter `cd /var/log` to change to the log directory.<br>b. Enter `grep "ROOT LOGIN" secure` to display the results of the root login.<br>c. Observe the login details displayed in the results.<br>d. Enter `clear` to clear the terminal screen. |
| 2. Generate a list of users with their login name and other details. | a. Enter `cd /etc` to change to the etc directory.<br>b. Enter `awk -F: {'print $1,$3,$6'}` `passwd` to list the login name, GID, and home directory for all users.<br>c. Observe the details displayed for the user accounts.<br>d. Enter `clear` to clear the terminal screen. |