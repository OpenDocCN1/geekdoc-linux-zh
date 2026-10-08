# 198

# csh

A pipeline or sequence can be enclosed within parentheses ( ) to form a simple command that can be a component in a pipeline or sequence.

A sequence of pipelines can be executed asynchronously or "in the background" by appending an ampersand (&); instead of waiting for the sequence to finish before issuing a prompt, the shell displays the job number ("Job Control" on page 206) and associated IDs and prompts immediately.

Note — Quote conventions are confusing. Overriding the escape character to force variable substitutions within double quotes is counterintuitive and inconsistent with the Bourne shell.

# History Substitution

History substitution enables you to use words from previous command lines in the command line you are typing. This process simplifies spelling corrections and the repetition of complicated commands or arguments. Command lines are saved in the history list, the size of which is controlled by the history variable. The most recent command is retained in any case. History substitution begins with a ! (although you can change this with variable) and occur anywhere on the command line; history substitutions do not nest. You can escape the with \ to suppress its special meaning.

Input lines containing history substitutions are echoed on the terminal after being expanded by any other substitutions take place or the command gets executed.

> — The g (global) flag in history substitutions applies only to the first match in each word, instead of to all matches in all words. The common text editors consistently do the latter when given the g flag in a substitution command.

Refer to history(1) for more details.

# Event Designators

An event designator is a reference to a command-line entry in the history list.

+   ! Start a history substitution, except when followed by a space character, Tab, newline, =, or (.
Refer to the previous command. By itself, this substitution repeats the previous command.
!n Refer to the command line n.\!-n Refer to the current command line minus n.
!str Refer to the most recent command starting with str.
!?str Refer to the most recent command containing str.
!?str additional Refer to the most recent command containing str, and append additional to that referenced command.
!(command) additional Refer to the most recent command beginning with command and append additional to that referenced command.