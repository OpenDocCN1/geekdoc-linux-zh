# Login shell

When you log in to the Linux system, the bash starts as a login shell. The login shell looks
for four different startup files to process commands from. The order in which the bash shell
processes the files is:

+   - /etc/profile
- $HOME/.bash_profile
- $HOME/.bash_login
- $HOME/.profile

The /etc/profile is the main default startup file for the bash shell on the system. Every
user on the system executes this startup file when they log in. The other three startup files are
specific for each user and can be customized for each user's requirements. Let's take a closer look
at these files.

# The /etc/profile file

The /etc/profile file is the main default startup file for the bash shell. Whenever you log in
to the Linux system, bash executes the commands in the /etc/profile startup file. Different
Linux distributions provide different commands in this file. On my Linux system, it looks like:

```
$ cat /etc/profile
# /etc/profile

# System wide environment and startup programs, for login setup
# Functions and aliases go in /etc/bashrc

pathmerge () (
  if ! echo $PATH | /bin/egrep -q "([^|:)$1(|:)"; then
    if [ "$2" = "after" ]; then
      PATH=$PATH:$1
    else
      PATH=$1:$PATH
    fi
)

# ksh workload
if [ -z "$EUID" -a x /usr/bin/id ]; then
  EUID=`id -u`
  UID=`id -ru`
fi

# Path manipulation
```