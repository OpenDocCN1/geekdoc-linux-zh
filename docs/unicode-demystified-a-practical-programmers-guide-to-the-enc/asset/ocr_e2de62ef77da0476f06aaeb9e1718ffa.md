Chapter 11 The emacs Editor

# Did You Modify a Buffer by Mistake?

It is usually during CONTROL-X s that you discover whose buffers were modified by mistake, and now emacs wants to save the wrong changes back to the file. Do not answer y if you are not sure. First get done with the CONTROL-X s dialog by typing n to any saves you are not clear about. Then you have options.

+   - Save the suspicious buffer into a temporary file with CONTROL-CONTROL-W, and analyze it later.
- Undo the changes with a string of CONTROL-, until the ** indicator disappears from the buffer's Mode Line.
- If you are sure that all the changes are correct, use META~ revert-buffer to get a fresh copy of the file.
- Kill the buffer outright. Because it is modified, you are asked whether you are sure.
- Give the META~ (tilde) command to clear the modified condition and ** indicator. A subsequent CONTROL-X then believes that the buffer does not need to be written.

# You Can Exit without First Getting a Warning

Clearing the modified flag (META~) allows you to exit without saving a modified buffer with no warning. Be careful if you choose to use this technique.

# Buffers

An emacs buffer is a storage object that you can edit. It often holds the contents of a file but can also exist without being associated with any file. You can select one buffer at a time, designated as the current buffer. Most commands operate only on the current buffer, even when multiple windows show two or more buffers on the screen. For the most part each buffer is its own world: It has its name, its own modes, its own file associations, its own modified state, and may even have its own special key bindings. You can use the commands shown in Table 11-13 to create, select, and manipulate buffers.

# Work with Buffers

| CONTROL-X b | Prompts for a buffer name and selects it. If it does not exist, this command creates it first. |