+   ▾ Command pasting.
+   ▾ Aliases.
+   ▾ Abbreviating file paths.
+   ▾ Redirecting inputs and outputs.
+   ▾ Environment variables.

# ## Using Tab Completion

By pressing the Tab key, you can have the shell complete the command you are typing. You can also use Tab completion as a guide to commands if you are unsure of which command you want.

If only one command completes what you have typed, then the full command is entered automatically. However, you still need to add any options, arguments and files, and press the Enter key.

If more than one command completes what you typed, then a list of possible completions displays. You can use the list as a guide to commands. Or you can type another letter, press the Tab key, and display another list of completions.

For example, if you type chg then press the Tab key, the command chgrp is entered at the prompt. No other command completes chg.

On the other hand, if you type cha, you get the following list:

chage chat chattr

This time, these three command complete what you have typed.

# ## Using Command History

The .bash_history file in your home directory lists all the commands that you have entered from the command line.

You can use this file to re-enter commands that you have already used. This ability is useful if you are doing repetitive work, or if you have made a mistake and want to correct it without re-typing.