assigned from /etc/profile, then those settings can be enhanced or overridden by a user's personal files.

The bash command shell, for example, looks for a file called .bashrc in the current user's home directory whenever it starts up. Similarly, the tsh command shell looks for a file called .tshrc in the user's home directory. You may see a repeating theme here. Startup scripts and configuration files for various applications usually begin with a dot (.) character and end in the letters rc (which stands for run commands). You can supply initial default versions of these and other configuration files by placing them in the /etc/skel directory. When you run the useradd command, these scripts and configuration files are copied to the new user's home directory.

# Supplying initial .bashrc and .bash_profile files

By supplying your users with initial .bashrc and .bash_profile files, you give them a starting point from which they can further customize their shell environment. Moreover, you can be sure that files are created with the appropriate access permissions so as not to compromise system security.

The .bash_profile script is run each time the user starts a new bash shell and, in turn, runs the .bashrc script. So, security is a concern. The .bash_profile file sets the original PATH used by the user, so it is a good place to add directories containing binaries you want the user to be able to run at your location. You can also add other start-up programs you want to run automatically for every user. Here's an example of the .bash_profile file.

```
# .bash_profile
# Get the aliases and functions
if [ -f -/.bashrc ]; then
 . /.bashrc
fi

# User specific environment and startup programs
PATH=$PATH: $HOME/bin
export PATH
unset USERNAME
```

The .bashrc file is a good place to supply useful command aliases and additions to the command search path. Here's an example:

```
# .bashrc
# User specific aliases and functions
alias rms='rm -i'
alias cp='cp -i'
alias mv='mv -i'
```