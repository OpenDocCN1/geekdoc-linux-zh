# LAB 2.3

# # REDIRECTING STANDARD INPUT AND OUTPUT

+   ### LAB OBJECTIVES
After this lab, you will be able to:
- Redirect stdin and stdout (< and >)
- Control Clobbering! (>> and |)
- Redirect stderr (2>)
- Link file descriptors for Redirection (n&)
- Use a here document for stdin (<<)

Every command that the KornShell runs has three standard I/O devices that it can use as it executes:

| stdin | The standard input device, normally the user's keyboard. |
| stdout | The standard output device, normally the window in which ksh is running. |
| stderr | The standard error device, also normally the window in which ksh is running. Used for error messages. |