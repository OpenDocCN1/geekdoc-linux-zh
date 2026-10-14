# Table 8-3: Example .login Script (cont.)

| Command | Description |
|---|---|
| setenv EDITOR emacs | Specifies the emacs editor as the default editor when running a program that lets you edit a file. For example, various mail programs let you use an editor to compose and edit messages. |
| setenv MAILHOST boston | Specifies boston as your mail handling system. |
| setenv PRINTER sales | Specifies the printer sales as your default printer. |

# 8.2.2 Metacharacters

Table 8-4 describes C shell metacharacters (characters that have special meaning to the shell). The meaning of these metacharacters are grouped by interpretation when they appear in a shell script, in a Filename specification, when used to quote other characters, in an Input/Output specification, or when used to indicate variable substitution.

# Table 8-4: C Shell Metacharacters

| Metacharacter | Description |
|---|---|
| Syntactic | |
| : | Separates commands that should be executed sequentially. |
| | | Separates commands that are part of a pipeline. |
| && | Runs the next command if the current command succeeds. |
| || | Runs the next command if the current command fails. |
| ( ) | Groups commands to run as a separate process in a subshell. |
| & | Runs commands in the background. |
| File Name | |
| / | Separates the parts of a file's pathname. |
| ? | Matches any single character except a leading dot (.). |
| * | Matches any sequence of characters except a leading dot (.). |
| [ ] | Matches any of the enclosed characters. |