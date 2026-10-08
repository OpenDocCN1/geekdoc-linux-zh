# 158 THE EMACS EDITOR

next ambiguity; the Enter key (RET) completes names in the same way as Space, but executes a complete command immediately.

The function and variable names used inside Emacs are extensive and clear, which, however, does not impair the use of Emacs. On the contrary, the documentation is very good, so you can easily find any required function by apropos, while the typing effort is greatly reduced by the completion functions. In the following sections, the key combinations are all integrated with the corresponding commands in parentheses. For each key combination, you can view the command to be executed and describe documentation by pressing C-h (describe-key).

If the system or the Emacs crashes, the currently processed data is not lost. Emacs periodically saves its data in an auto-file (#file name*) which can be used to restore the data after a breakdown. When loading for an auto-save file exists, users are advised that they can restore modifications by means of the M-x recover-file command. If you have edited many files, you can restore the session Emacs presents a list of the previous sessions from which you can choose by moving the cursor to the corresponding line and pressing C-c C-c.

Creation of auto-save copies can be configured by means of a series of variables. If the variable auto-save-default is not nil, the auto-save function is activated for every new buffer. The variable auto-save-interval specifies after how many typed characters a backup copy is created. The variable auto-save-timeout is used to determine how many seconds without input an auto-save file is written.

Normally, the auto-save function is active when Emacs is started, and the variable auto-save-interval has a value of 300. If many characters were deleted in a buffer, Emacs deactivates the auto-save function, because it would be wasteful. You can, however, delete the buffer and reload the file, so that Emacs can again create auto-save copies.