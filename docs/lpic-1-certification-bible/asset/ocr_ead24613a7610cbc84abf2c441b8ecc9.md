Table 14-6 
 Search Commands
| Command | Function |
|---------|----------|
| fa | Searches for the first instance of a to the right of the cursor. |
| Fa | Searches for the first instance of a to the left of the cursor. |
| ta | Moves to the character to the left of the next a. |
| Ta | Moves to the character to the right of the first preceding a. |
| ; | Repeats the last f, F, t, or T command. |
| , | Same as ;, but reverses the direction of the search. |
| /string | Searches to the right for the first instance of string. |
| ?string | Searches to the left for the first instance of string. |
| n | Repeats the last / or ? search. |
| N | Repeats the last / or ? search, but in the opposite direction. |
| :% | Searches the entire file. |
| :..$ | Searches from the current cursor position to the end of the file. |
| :1,5 | Searches lines one through five. |

# ### Undoing changes

We all make mistakes, and luckily vi lets you undo changes you have made. To undo the last command, use the `u` command. To undo all changes made to the current line use the `U` command. If you have really messed up, you can revert back to the last saved copy of a file with the `:e!` command.

# ## Customizing the Shell Environment

+   - **Customize and use the shell environment.** Customize your shell environment: set environment variables (e.g. PATH) at login or when spawning a new shell; write bash functions for frequently used sequences of commands. Involves editing these files in your home directory: `bash_profile` | `.bash_login` | `.profile` ; `bashrc` ; `.bash_logout` ; `.inputrc`

# **1.9** Shells, Scripting, Programming, Compiling