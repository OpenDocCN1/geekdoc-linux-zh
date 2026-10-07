We will regularly update the Web site with information about this text and future work on Solaris Internals. We will place information about the differences between Solaris 7 and 8 at this URL, post any errors that may surface in the current edition, and share reader feedback and comments and other bits of related information.

# Notational Conventions

Table P-1 describes the typographic conventions used throughout the book, and Table P-2 shows the default system prompt for the utilities we describe.

**Table P-1** Typographic Conventions

| Typeface or Symbol | Meaning | Example |
| --- | --- | --- |
| AaBbCc123 | Command names, file names, and data structures | The vmstat command. The <sys/proc.h> header file. The proc structure. |
| AaBbCc123 () | Function names. | page_create_va() |
| AaBbCc123(2) | Manual pages. | Please see vmstat(1M). |
| AaBbCc123 | Commands you type within an example. | $ vmstat swap free re mf 0 0 0 46440 18920 1 13 |
| AaBbCc123 | New terms as they are introduced. | A major page fault occurs when... |

**Table P-2** Command Prompts

| Shell | Prompt |
| --- | --- |
| C shell prompt | machine_name% |
| C superuser prompt | machine_name# |
| Bourne and Korn shell prompt | $ |
| Bourne shell and Korn shell superuser prompt | # |
| The crash utility prompt | crash > |