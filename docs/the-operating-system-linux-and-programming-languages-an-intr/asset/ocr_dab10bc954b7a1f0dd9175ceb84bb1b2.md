locate search expression. Lists all files and directories in the local database, which correspond to the search expression. Extremely well suited to search for files (if the database is frequently updated → system administrator)

find searches recursively for files corresponding to search expression within the given path.
Example: find . -name '*.txt' searches recursively for all *.txt files, starting within the current directory.

grep searches for text within given files.
Example: grep 'test' ../*.f90 searches for the text test in all *.f90 files in the parent directory.
The most important option is [-i], which forces grep to ignore any distinction between upper and lower case.

# 5 UNIX shells

The shell is a service program through which the user communicates with the OS and which is responsible for the interpretation of the input commands.

# Different UNIX shells

Since the shell does not directly belong to the OS, a number of different shells have been developed in the course of time:

+   - Bourne shell (sh). A well-known and widespread shell, named after its inventor Steven Bourne. An advanced derivate, the bash, Bourne again shell (note the pun) is most popular under Linux.
+   - C-Shell (csh). Developed in Berkeley, and uses a more C-like syntax. An improved version of the C-shell is the tcsh.
+   - Bash shell (bash). Advanced Bourne shell and standard on many systems.

Each shell contains a set of system variables, which can be augmented by user-defined variables. This set comprises the process environment for the programs running inside the shell.

Moreover, the shell can be used to run (system-) programs via shell scripts.