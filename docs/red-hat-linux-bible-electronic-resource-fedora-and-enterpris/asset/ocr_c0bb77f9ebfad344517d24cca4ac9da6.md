Table 4-3 lists the keystrokes for cutting and pasting text on a command line.

# Table 4-3: Keystrokes for Cutting and Pasting Text in
Command Lines

| Keystroke | Full Name | Meaning |
|---|---|---|
| Ctrl+k | Cut end of line. | Cut text to the end of the line. |
| Ctrl+u | Cut beginning of line. | Cut text to the beginning of the line. |
| Ctrl+w | Cut previous word. | Cut the word located behind the cursor. |
| Alt+d | Cut next word. | Cut the word following the cursor. |
| Ctrl+y | Paste recent text. | Paste most recently cut text. |
| Alt+y | Paste earlier text. | Rotate back to previously cut text and paste it. |
| Ctrl+c | Delete whole line. | Delete the entire line. |

# Command line completion

To save you a few keystrokes, the bash shell offers several different ways of completing partially typed values. To attempt to complete a value, type the first few characters, and then press Tab. Here are some of the values you can type partially:

+   - **Environment variable** — If the text begins with a dollar sign ($), the shell completes the text with an environment variable from the current shell.
+   - **User name** — If the text begins with a tilde (~), the shell completes the text with a user name.
+   - **Command, alias, or function** — If the text begins with regular characters, the shell tries to complete the text with a command, alias, or function name.
+   - **Host name** — If the text begins with an at (@) sign, the shell completes the text with a host name taken from the /etc/hosts file.

> **TIP:** To add host names from an additional file, you can set the HOSTFILE variable to the name of that file. The file must be in the same format as /etc/hosts.

Here are a few examples of command completion. (When you see <Tab>, it means to press the Tab key on your keyboard.) Type the following:

```
```
$ echo $OS<Tab>
$ cd ~ro<Tab>
```
```