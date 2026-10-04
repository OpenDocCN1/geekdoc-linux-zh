# Text Editing with ed and vi 201

For example, Fedora Core refuses to boot from the hard drive, you may have to boot from a floppy disk. In that case, you have to edit system files with the ed editor because editor is small enough to fit on the floppy. I walk you through the basic text-editing commands of ed and vi. You'll see — they're not that hard.

# Using ed

Typically, you have to use ed only when you boot a minimal version of Linux (for example, from a floppy you've set up as a boot disk), and the system doesn't support full-screen mode. In all other situations, you can use the ed editor that works in full-screen text mode.

When you use ed, work in each command mode or text-input mode:

+   **Command mode** is what you get by default. In this mode, anything that you type is interpreted as a command. The ed editor has a simple set where each command contains one or more characters.
**Text-input mode** is for typing text. You can enter input mode with the commands a (append), c (change), or i (insert). After entering lines of text, you can leave input mode using a period (.) on a line by itself.

To practice editing a file, copy the /etc/fstab file to your home directory by issuing the following commands:

```
cd
cp /etc/fstab .
```

Now you have a file named fstab in your home directory. Type the command to begin editing a file in ed:

```
ed -p: fstab
783
:
```

This example uses the -p option to set the prompt to the colon character (:) and opens the fstab file (in the current directory, which is your home directory) for editing. The ed editor opens the file, reports the number of characters in the file (783), displays the prompt (:), and waits for a command.

![](bbox=[0.135, 0.788, 0.195, 0.853])

TIP When you're editing with ed, make sure you always turn on a prompt character (use the -p option). Without the prompt, distinguishing whether ed is in input mode or command mode