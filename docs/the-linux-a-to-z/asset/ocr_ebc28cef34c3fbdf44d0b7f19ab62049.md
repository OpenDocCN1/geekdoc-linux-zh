+   - When this file transfer has finished, you can request the transfer of further files just by issuing more `get` commands. After you have got all the files you want you can switch the remote `kermit` out of server mode and back into interactive mode with the command:

    `finish`

When the server has shut down, you will get a `kermit>` prompt from the local machine. If at this point you issue a `connect` command then it will switch your local `kermit` back into being a terminal emulator and you will get another `kermit>` prompt, but this time from the remote machine.
- Typing the command:

    `quit`

will now terminate the remote `kermit` and return you to a shell prompt from the remote machine.
- When you have finished with your terminal session on the remote machine you should log off. You then type the escape sequence to get back to the `kermit>` prompt from your local machine. Finally, typing the `quit` command to this prompt will terminate the local `kermit` and return you to a shell prompt.

There are many more options to `kermit` than you have seen here, but this should have given you the basic idea. For more information there is a fairly comprehensive help facility built into `kermit` itself, which you can access just by typing `help` to a `kermit>` prompt.