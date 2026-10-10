| Keystroke | Full Name | Meaning |
| --- | --- | --- |
| Alt+u | Uppercase word | Change the current word to uppercase. |
| Alt+I | Lowercase word | Change the current word to lowercase. |
| Alt+c | Capitalize word | Change the current word to an initial capital. |
| Ctrl+v | Insert special character | Add a special character. For example, to add a Tab character, press Ctrl+v+Tab. |

Table 4-3 lists the keystrokes for cutting and pasting text on a command line.

# ## Table 4-3: Keystrokes for Cutting and Pasting Text in Command Lines

| Keystroke | Description |
| --- | --- |
| Ctrl+k | Cut text to the end of the line. |
| Ctrl+u | Cut text to the beginning of the line. |
| Ctrl+w | Cut the word located behind the cursor. |
| Alt+d | Cut the word following the cursor. |
| Ctrl+y | Paste most recently cut text. |
| Alt+y | Rotate back to previously cut text and paste it. |
| Ctrl+c | Cancel the entire command line. |

# ## Command-line completion

To save you a few keystrokes, the bash shell offers several different ways of completing partially typed values. To attempt to complete a value, type the first few characters, and then press Tab. Here are some of the values you can type partially:

+   1.  **Enviroment variable** — If the text begins with a dollar sign ($), the shell completes the text with an environment variable from the current shell.

+   1.  **User name** — If the text begins with a tilde (~), the shell completes the text with a user name. (This is actually just a case of file or directory expansion. For example, `~chr` might expand to `~chris/`, which would identify the home directory `/home/chris/`.)

+   1.  **Command, alias, or function** — If the text begins with regular characters, the shell tries to complete the text with a command, alias, or function name.

+   1.  **Filenames** — After a command has been typed, anything beginning with a `/` or regular characters is completed as a path to a directory or filename. This is one of the most common forms of command-line completion because it can help you traverse directory paths with long names or complete long filenames.

+   1.  **Hostname** — If the text begins with an at (@) sign, the shell completes the text with a hostname taken from the `/etc/hosts` file.