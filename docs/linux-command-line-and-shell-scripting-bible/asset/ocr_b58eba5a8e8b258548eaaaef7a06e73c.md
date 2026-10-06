# Part IV Alternative Linux Shells

The zsh shell provides a core set of built-in commands, plus the ability to add additional command modules. Each command module provides a set of additional built-in commands for specific circumstances, such as network support and advanced math functions. You can add only the modules you think you need for your specific situation.

This feature provides a great way to either limit the size of the zsh shell for situations that require a small shell size and few commands, or expand the number of available built-in commands for situations that require faster execution speeds.

# Parts of the zsh Shell

This section walks through the basics of the zsh shell, showing the built-in commands that are available (or can be added by installing modules), as well as the command line parameters and environment variables used by the zsh shell.

# Shell options

Most shells use command line parameters to define the behavior of the shell. The zsh shell uses a few command line parameters to define the operation of the shell, but mostly it uses options to customize the behavior of the shell. You can set shell options either on the command line, or within the shell itself using the set command.

Table 23-1 lists command line parameters available for the zsh shell.

While this may seem like a small set of command line parameters, the -o parameter is somewhat misleading. It allows you to set shell options that define features within the shell. By far the zsh shell is the most customizable shell available. There are lots of features that you can alter for your shell environment. The different options fit into several general categories:

+   - Changing directories: Options that control how the cd and dirs commands handle directory changes
- Completion: Options that control command completion features
- Expansion and globbing: Options that control file expansion in commands
- History: Options that control command history recall
- Initialization: Options that control how the shell handles variables and startup files when started
- Input/Output: Options that control command handling
- Job Control: Options that dictate how the shell handles and starts jobs
- Prompting: Options that define how the shell works with command line prompts
- Scripts and Functions: Options that control how the shell processes shell scripts and defines shell functions