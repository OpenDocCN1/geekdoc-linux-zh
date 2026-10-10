# ftp

**ftp** \[ *option* \] \[ *host* \]
Establishes a File Transfer Protocol (FTP) connection with the specified host and launches an interactive utility that enables you to download (get) or upload (put) files from FTP servers (assuming that you have the appropriate permissions). See the Commands table for the commands that you can use in the interactive session.

# OPTIONS

| Use This Option | To Do This |
| :---------------- | :-------------------------------------------------------------------------- |
| `-d` | Enable debugging |
| `-e` | Disable command editing and history support |
| `-g` | Disable filename globbing |
| `-l` | Turn off interactive prompting during multiple file transfers |
| `-n` | Refrain from attempting auto-login upon initial connection |
| `-p` | Use passive mode for data transfers |
| `-v` | Show all responses from the remote server and report data transfer statistics |

# COMMANDS

| Use This Option | To Do This |
| :---------------- | :-------------------------------------------------------------------------- |
| `$ macro [ argument ]` | Execute the macro that was defined with the **macrodef** command. |
| `? [ command ]` | Display help for the specified command. |
| `! [ command [ argument ] ]` | Start an interactive shell on the local machine. Optionally, you can specify an argument. |
| `account [ password ]` | Start a supplementary login after the primary login has been successfully completed. You can optionally specify a password. |