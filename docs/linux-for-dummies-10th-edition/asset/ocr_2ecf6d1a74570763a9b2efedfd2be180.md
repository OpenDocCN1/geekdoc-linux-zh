| Environment Variable | Purpose | Value |
| :--- | :--- | :--- |
| HISTSIZE | Determines the number of previously typed commands that are stored. | Number of commands |
| HOME | Sets the location of your home directory. | The path to your home directory |
| MAILCHECK | Sets how often the bash shell checks for new mail in your mailbox. If mail has arrived, you see a message similar to `You have new mail` the next time you do something at the command prompt. | Number of seconds to wait between checks |
| PATH | Sets the directories that bash looks in, and the order to look in them to find a program name you type at the command prompt. | Colon-separated directories |
| PS1 | Sets your command prompt. | Command and formatting characters used to form the prompt |

Most environment variables are established for you by the system Administrator or perhaps by the shell itself. These variables are mostly read by programs to gather information, and you don't need to change their values. However, you may want to alter the value of some environment variables. For example, in Table 16-1, the first entry, `HISTSIZE`, determines the number of lines of command line history that are kept on file. You may have read the discussion, earlier in this chapter, of re-executing a command from yesterday. (If not, refer to the section "Accessing your command history.") By setting a higher number for `HISTSIZE`, you can save an even longer list of previously executed commands.

# ## Storing and retrieving variables' values

To assign a value to a variable, you just use the variable name followed by an equal sign (=), followed by the value to store:

```
`MyVariable=MyValue`
```

To retrieve the value represented by that variable, you need to precede the variable name with a dollar sign ($). Look at a variable, created by the shell, that determines what your prompt looks like. This variable is named `PS1`. First, you view the value being held by `PS1`:

```
`echo $PS1`
```