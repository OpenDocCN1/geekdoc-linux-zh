This shell is nearly compatible with commercial versions of the Korn shell included with commercial UNIX distributions. Documentation for this shell is in the ksh manual page and in the pdksh directory (under the /usr/doc/pdksh directory).

# Features of the csh-Compatible Shell—tcsh

The tcsh shell, by William Joy (and 47 other contributors), features 53 built-in commands and 18 command-line options. This shell emulates the csh shell but has many more features, including a command-line editor with spelling correction.

This shell is not only compatible with the bash shell prompts; it offers more prompt options than bash. tcsh uses the file csh.cshrc under the /etc directory (much like bash's /etc/profile) if the .tcshrc or .cshrc resource files do not exist in your home directory. Like the bash shell, you can scroll through commands you've entered and edit the command line.

Get a list of the tcsh commands by using the builtins command (tcsh does not have help like the bash shell), as follows:

```
# builtins
:       @       alias     alloc     bg      bindkey  break
breaksw builtins case      cd        chdir   complete continue
default dirs    echo      echotc    else    end      endif
endsw   eval    exec      exit      fg      filetest foreach
glob    goto    hashstat  history   hup     if       jobs
kill    limit   log       login     logout  ls-F     nice
nohup   notify  onintr    popd      printenv pushd    rehash
repeat  sched   set       setenv    setty   shift
source  stop    suspend   switch    telltc  time     umask
unalias uncomplete unhash   unlimit   unset   unsetenv wait
where   which   while
```

For more information about this shell, read the tcsh manual page, or look in the tcsh directory under the /usr/doc/tcsh directory to see a Frequently Asked Questions (FAQ) file and other text files.

# zsh

The zsh shell, originally created by Paul Falstad, is one of the largest shells for Linux and features 84 built-in commands. The zsh shell has more than 50 different command-line options and also emulates the sh and ksh shell commands.

Like the bash and tcsh shells, the zsh shell enables you to scroll through previous commands and complete, edit, or spell-check the command line. It also enables you to use job control to manage running programs. This shell features advanced command-line options for searching or matching file patterns.