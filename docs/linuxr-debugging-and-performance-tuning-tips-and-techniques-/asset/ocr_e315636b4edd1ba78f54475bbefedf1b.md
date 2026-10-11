16.1 Project Description

+   How will you handle putting commands in the background? What about waiting for a command in the background to finish?

+   Decide whether you will have shell variables.

+   What kind of wildcarding or other expansions will you support? How do they interact with quoting? With shell variables?

+   You should plan for at least an if and a while statement. Design a syntax. We will call these block statements.

+   Decide whether or not you wish to allow I/O redirection for a block statement. If yes, what will the syntax look like?

+   Decide how, if at all, your shell language should handle signals.

+   Design a testing and debugging framework before you start to code.

+   If you're going to use `i18n` facilities, do so from the outset. Retrofitting them in is painful.

+   For the real work, start simply. The initial version should read one line at a time and break it into words to use as separate arguments. Don't do any quoting, I/O redirection, or anything else. Don't even try to create a new process to run the entered program. How are you going to test what you have so far?

+   Add quoting so that individual "words" can contain whitespace. Does the quoting code implement your design?

+   Make your built-in commands work. (See Section 4.6, "Creating Files," page 106, and Section 8.4.1, "Changing Directory: `chdir()` and `fchdir()`," page 256, for at least two necessary built-in commands.) How are you going to test them?

+   Initially, use a fixed search path, such as "/bin;/usr/bin;/usr/local/bin". Add process creation with `fork()` and execution with `exec()` (see Chapter 9, "Process Management and Pipes," page 283). Starting out, the shell should wait for each new program to finish.

+   Add backgrounding and, as a separate command, waiting for process completion (see Chapter 9, "Process Management and Pipes," page 283).

+   Add a user-settable search path (see Section 2.4, "The Environment," page 40).

643