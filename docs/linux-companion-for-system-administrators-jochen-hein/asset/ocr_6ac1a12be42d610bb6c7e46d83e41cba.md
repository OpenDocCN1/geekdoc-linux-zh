# USER-RELATED CONFIGURATION 145

Therefore, when a new user ID is created, a standard environment is installed. The required files should be stored in the directory /etc/sk and can be copied manually or by means of a script (see also the useradd program) into the home directory of the new user. Obviously, the new user should become the owner of these files so he/she can later adapt them to his/her personal requirements.

Modern shells use the tilde (-) to refer to the home directory of a user. However, only access via the environment variable HOME is portable and, for example, usable in sh scripts. The cd (chdir, change directory) command without parameters always changes back into the home directory, by the pwd command (print working directory) may be used to display the current directory. This command is often an internal command of the shell, for reasons of compatibility with the POSIX.2 standard, there is also a program /bin/pwd.

The names of most configurations begin with a dot (.), so that these files are not shown by ls. To display all files, the -a option (or --all) GNU ls must be specified.

# 4.11.1 Selection of an interactive shell

When logging in a text terminal or console, the shell specified in the file /etc/passwd is started. This will usually be a program, such as the bash or the tcsh. This shell is also started by xterm if no program name is specified as a parameter. The shell is the first interface a user encounters on a UNIX system. The use of an interactive shell is very important for efficient work.

For interactive work, generally a shell is used which allows editing of the command line and which has a history function. Command and file name completion are additional useful functions. Frequently, alias names are used to abbreviate long commands or automatically specify special options.

# The csh or tcsh

The csh (or tcsh) is often used as a login shell. It is well suited for interactive work and has practically all functions one would expect from a shell. However, it is not the 'optimum' shell, since there are tasks this shell cannot perform. An extensive description of the disadvantages of the csh can be found in the text 'Why csh is considered harmful' by Tom Christiansen (tchrist@mox.perl.com). This text is posted regularly, for example, in the newsgroup comp.unix.shell and can be found in the FAQ archive of rtfm.with.edu.