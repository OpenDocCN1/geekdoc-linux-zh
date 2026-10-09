```
```bash
$ cat ~/.bash_profile
if [ -f ~/.bashrc ]; then
    . ~/.bashrc                          # Read local startup file if it exists
fi
PATH=$PATH:/usr/local/bin               # Add /usr/local/bin to PATH
export PS1='\h \w \u\$'
```

```

The first command in the preceding **bold** .bash_profile file executes the commands in the user’s .bashrc file if it exists. The next command adds to the PATH variable (page 359). Typically PATH is set and exported in /etc/profile, so it does not need to be exported in a user’s startup file. The final command sets and exports PS1 (page 361), which controls the user’s prompt.

The first command in the .bashrc file shown below executes the commands in the /etc/bashrc file if it exists. Next the file sets noclobber (page 156), unsets MAILCHECK (page 361), exports LANG (page 366) and viminit (for vim initialization), and defines several aliases. The final command defines a function (page 396) that swaps the names of two files.

```
```bash
$ cat ~/.bashrc
if [ -f /etc/bashrc ]; then
    source /etc/bashrc                  # read global startup file if it exists
fi

set -o noclobber                        # prevent overwriting files
unset MAILCHECK                         # turn off "You have new mail" notice
export LANG=C                           # set LANG variable
export viminit='set ai aw'              # set vim options
alias df='df -h'                        # set up aliases
alias rm='rm -i'                       # always do interactive rm's
alias lt='ls -ltrh | tail'
alias hw='history | tail'
alias ch='chmod 755 '

function switch() {                     # a function to exchange
    local tmp=$$switch                 # the names of two files
    mv "$1" $tmp
    mv "$2" "$1"
    mv $tmp "$2"
}
```
```

![](bbox=[0.06, 0.76, 0.11, 0.79])

# . (Dot) or source: Runs a Startup File in the Current Shell

After you edit a startup file such as .bashrc, you do not have to log out and log in again to put the changes into effect. Instead, you can run the startup file using the . (dot) or source builtin (they are the same command). As with other commands, the . must be followed by a space on the command line. Using . or source is similar to running a shell script, except these commands run the script as part of the current process. Consequently, when you use . or source to run a script, changes you make to variables from within the script affect the shell you run the script from. If you ran a startup file as a regular shell script