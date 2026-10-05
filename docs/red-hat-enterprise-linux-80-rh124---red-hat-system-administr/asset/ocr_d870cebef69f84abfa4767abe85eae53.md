# CHAPTER 2 | Creating, Viewing, and Editing files

> IMPORTANT\By convention, environment variables and shell variables that are automatically set by the shell have names that use all uppercase characters. If you are setting your own variables, you may want to use names made up of lowercase characters to help avoid collisions.

# SETTING VARIABLES AUTOMATICALLY

If you want to set shell or environment variables automatically when your shell starts, you can edit the Bash startup scripts. When Bash starts, several files contain shell commands that initialize the environment.

The scripts that run depend on how the shell was started, whether it is an interactive login shell, an interactive non-login shell, or a shell script.

Assuming the default /etc/profile,/etc/bashrc and ~/.bash_profile, if you want to make a change to your user account that affects all your interactive profiles at startup, edit your .bashrc file. For example, you can set that account's default editor to nano by editing the file:

```
# .bashrc
# Source global definitions
if [ -f /etc/bashrc ]; then
  /etc/bashrc
fi

# User specific environment
PATH="$HOME/.local/bin:$HOME:$PATH"
export PATH

# User specific aliases and functions
export EDITOR=nano
```

> NOTE
The best way to adjust settings that affect all user accounts is by adding a file with a name ending in .sh containing the changes to to the /etc/profile.d directory. To do this, you need to be logged in as the root user.

# UNSETTING AND UNEXPORTING VARIABLES

To unset and unexport a variable, use the unset command:

```
[user@host] $' echo file1
/tmp.z9pXW0qc
[user@host] ~$ unset file1
[user@host] ~$ echo file1

[user@host]$
```