
# Set shell variables
set noclobber
set ignoreeof
set notify

# Set command aliases
alias h 'history \!* | more'
alias l 'ls -l'
alias c clear

# Set history variables
set history=40
set savehist=40

# Set prompt
set prompt = "!" $ 

## Table 8-2: Example .cshrc Script

| Command | Description |
|---|---|
| Shell Variables | |
| set noclobber | Stops files from being overwritten. If set, places restrictions on output redirection > to ensure that files are not accidentally destroyed, and that >> redirections refer to existing files. |
| set ignoreeof | Specifies that you cannot use Ctrl/D to end your login session. Instead, you must use either the exit or the logout commands. |
| set notify | Informs you when background processes have completed. |
| Command Aliases | |
| alias h 'history \!* | more' | Defines the contents of the command history buffer through the more command. The \!* string specifies that all the history buffer should be piped. |
| alias l 'ls -l' | Defines a short name, l, for the ls -l command that lists directory files in the long format. |
| alias c clear | Defines a short name, c, for the clear command that clears your screen. |
| History Variables | |
| history=40 | Instructs the shell to store the last 40 commands in the history buffer. |
| savehist=40 | Instructs the shell to store the last 40 commands and use them as the starting history for the next login session. |
| Prompt Variable | |
| set prompt = "\! $ " | Changes your prompt so that it tells you the command number of the current command. |

In the following .login script, the permissions for file creation are set, the PATH environment variable is set, and the editor and printer are specified. Table 8-3 explains each part of the script.

```
# Set file creation permissions
umask 027

# Set environment variables
set path=/usr/bin:/usr/local/bin:
set cdpath=.:..:$HOME
setenv EDITOR emacs
setenv MAILHOST boston
setenv PRINTER sales
```

## Table 8-3: Example .login Script

| Command | Description |
|---|---|
| File Permissions | |
| umask 027 | Specifies the permissions to be subtracted from the default permissions set by the creating program for all new files created. The umask value is subtracted from 777 (for executable programs) or from 666. For an executable program, a umask value of 027 results in all permissions for the owner, read and execute permissions for members of the same group, and no permissions for all others. |
| Environment Variables | |
| set path /usr/bin:/usr/local/bin: | Specifies the search path. In this case, /usr/bin is searched first, and /usr/local/bin is searched second. |
| set cdpath=.:..:$HOME | The cdpath variable sets the search path for the cd command. This variable assignment specifies that the cd command should search for the named directory in the current directory (.) first, in the parent directory (..) second, and the home directory ($HOME) third. |
| setenv EDITOR emacs | Specifies the emacs editor as the default editor when running a program that lets you edit a file. For example, various mail programs let you use an editor to compose and edit messages. |
| setenv MAILHOST boston | Specifies boston as your mail handling system. |
| setenv PRINTER sales | Specifies the printer sales as your default printer. |

## 8.2.2 Metacharacters

Table 8-4 describes C shell metacharacters (characters that have special meaning to the shell). The meaning of these metacharacters are grouped by interpretation when they appear in a shell script, in a Filename specification, when used to quote other characters, in an Input/Output specification, or when used to indicate variable substitution.

## Table 8-4: C Shell Metacharacters

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
