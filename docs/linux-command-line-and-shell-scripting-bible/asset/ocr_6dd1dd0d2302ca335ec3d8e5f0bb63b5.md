# Part IV Alternative Linux Shells

The zsh shell modules cover a wide range of topics, from providing simple command line editing features to advanced networking functions. The idea behind the zsh shell is to provide a basic minimum shell environment and let you add on the pieces you need to accomplish your programming job.

# Viewing, adding, and removing modules

The zmodload command is the interface to the zsh modules. You use this command to view, add, and remove modules from the zsh shell session.

Using the zmodload command without any command line parameters displays the currently installed modules in your zsh shell:

```
% zmodload
zsh/zutil
zsh/complete
zsh/main
zsh/terminfo
zsh/zie
zsh/parameter
%
```

Different zsh shell implementations include different modules by default. To add a new module, just specify the module name on the zmodload command line:

```
% zmodload zsh/zftp
%
```

 indicates that the module loaded. You can perform another zmodload command, and the new module should appear in the list of installed modules.

Once you load a module, the commands associated with the module are available as built-in commands:

```
% zftp open myhost.com rich testing
Welcome to the myhost FTP server.
% zftp cd test
% zftp dir
01-21-08 11:21PM  120823 test1
01-21-08 11:23PM  118432 test2
% zftp get test1 > test1.txt
% zftp close
%
```

The zftp command allows you to conduct a complete Ftp session directly from your zsh command line! You can incorporate these commands into your zsh shell scripts to perform transfers from your scripts.

To remove an installed module, use the -u parameter, along with the module name:

```
% zmodload -u zsh/zftp
% zftp
```