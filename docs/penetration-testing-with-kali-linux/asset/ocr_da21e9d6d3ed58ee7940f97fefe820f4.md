# OffSec

Although these tools perform many automated checks, we should bear in mind that every system is different, and unique one-off system changes will be missed by these types of tools. For this reason, it's important to check for unique configurations that can only be caught by manual inspection, as illustrated in the previous section.

In the next Unit we are going to learn how to act on the information we obtained through enumeration to elevate our privileges.

# 17.2 Exposed Confidential Information

This Learning Unit covers the following Learning Objectives:

+   * Understand user history files
* Inspect user trails for credential harvesting
* Inspect teams for credential harvesting

In this Learning Unit we are going to inspect how user and service history files constitute the initial stage of privilege escalation, often leading to the desired outcome.

# 17.2.1 Inspecting User Trails

As penetration testers, we are often time-constrained during our engagements. For this reason, we should focus our efforts on low-hanging fruit.

One target is users' history files. These files often hold clear-text user activity that might include sensitive information such as passwords or authentication method.

On Linux, applications frequently store user-specific configuration files and subdirectories within a user's home directory. These files are often called dotfiles because they are prepended with a period. The prepended dot character instructs the system not to display these files when listing command.

One example is bashrc. The .bashrc script is executed when a new terminal is opened from an existing login session or when a new instance is started from an existing login session. From this script, additional environment variables can be specified automatically whenever a new user's shell is spawned.

Sometimes administrators store credentials inside environment variables as a way to interact with custom scripts that require authentication.

Reviewing our target Debian, we'll notice an unusual environment variable entry:

```
joe@debian-presvesc:~$ env
XDG_SESSION_CLASS=user
TERM=xterm-256color
SCRIPT_CREDENTIALS=lab
USER=joe
LC_TERMINAL_VERSION=3.4.16
```