# 212

# csh

popd [+n] Pop the directory stack and change to the new top directory. The elements of the directory stack from 0, starting at the top. When you specify +n, discard the n-th entry in the stack.

pushd [+n] dir Push a directory onto the directory stack. With no arguments, exchange the top two elements. When you specify +n, rotate the n-th entry to the top of the stack and change to it. With dir-argument, push the current working directory onto the stack and change to dir.

rehash Recompute the internal hash table of the contents of directories in the path variable to account for new commands. Recompute the internal hash table of the contents of directories listed in the cpath variable to account for new directories.

repeat command Repeat command count times. command is subject to the same restrictions as with the one-line if statement.

set [var = value]

set var[n] With no arguments, display the values of all shell variables. Display multiword values as a parenthesized list. With the argument alone, assign an empty (null) value to the var variable. With arguments of the form var = value, assign value to var, where value is of:

+   word A single word (or quoted string).
(wordlist) A space-separated list of words enclosed in parentheses.

Values are command and file-name expanded before being assigned. The set var[n] = word replaces the n-th word in a multword with word

setenv [VAR] With no arguments, display all environment variables. With the VAR argument, set the environment variable VAR to have an empty (null) value. By convention, environment variables are normally given uppercase names. With both word and VAR arguments, set the environment variable NAME to the value which must be either a single word or a quoted string. The most commonly used environment variables, USER, TERM, and PATH, are automatically imported to and exported from the csh variables, term, and path; you do not need to use setenv for these. In addition, the shell sets the PWD environment variable from the csh variable cwd whenever the latter changes.

The environment variables LC_TYPE, LC_MESSAGES, LC_TIME, LC_NUMERIC, and LC_MONETARY take immediate effect when changed within the C shell.