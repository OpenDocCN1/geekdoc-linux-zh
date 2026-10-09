# Procedure Reference: Compare Files in the GUI

To compare files in the GUI:

+   1. Press Ctrl+Alt+F7 to switch to the GUI.
2. From the menu bar, choose Application→Accessories→Terminal.
3. Enter gvimdiff {file_name_1} {file_name_2} to compare files for differences in content.
4. Enter :q two times to return to the terminal.

# Procedure Reference: Replace Characters

To replace characters:

+   1. Log in as a user in the CLI.
2. Replace characters.

+   • Enter tr {'character_1'} {'character_2'} < {file_name} to replace one character with another one in the given file.
• Enter {command} | tr {'condition_1'} {'condition_2'} to replace one character with another one from the output of the command.

# Working with Multiple Windows

You can choose to tile your windows horizontally or vertically. Press Ctrl+W+V to create a vertical split, or press Ctrl+W+S to split the screen horizontally.