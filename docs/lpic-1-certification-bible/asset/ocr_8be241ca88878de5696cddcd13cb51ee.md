Table 14-14  
**shopt Options**
| Option | Function |
| --- | --- |
| c d a b l e _ v a r s | If set, an argument to the cd command that is not a valid directory is assumed to be a variable with a value of the directory you want to change to. |
| c d s p e l l | If set, minor spelling errors when using cd in directory names will be corrected. |
| c h e c k h a s h | If set, bash first checks to see if an executable listed in the hash table exists before executing. If it no longer exists, a standard path search is done. |
| c m d h i s t | If set, bash attempts to save all lines of a multiple-line command in the same history entry. |
| d o t g l o b | If set, bash includes filenames beginning with a . in the results of path name expansion. |
| h i s t a p p e n d | If set, the history list is appended to the history file at exit, instead of overwriting it. |
| m a i l w a r n | If set, if bash does a mail check and notices that the mail file has been accessed since the last check, a warning is issued. |

# # Writing Simple Scripts

# **1.9 Shells, Scripting, Programming, Compiling**

+   *   **Customize or write simple scripts.** Customize existing scripts (like paths in scripts of any language), or write simple new ( *bash* ) scripts. Besides use of standard *sh* syntax (loops, tests), be able to do things like: command substitution and testing of command return values, test of file status, and conditional mailing to the superuser. Make sure the correct interpreter is called on the first ( *#!* ) line, and consider location, ownership, and execution- and suid-rights of the script.

Shell scripts are used to execute several commands in a sequence. They are similar to batch files in the Microsoft world, but provide much more power and control. They are stored as text files and can be as simple as a list of commands to execute or can utilize much more complex functions and structures.