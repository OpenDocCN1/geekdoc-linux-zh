# Shell Features

This chapter functions as a reference source for C shell and Bourne, Korn, or POSIX shell features. Unlike other chapters of this guide that present conceptual or tutorial information, or both, the purpose of this chapter is to provide very brief reference information about each shell.

To get the most out this chapter, you already should be familiar with the introductory shell overview information in Chapter 7.

After completing this chapter, you should be able to:

+   - Understand the main differences between operating system shells
+   - Understand specific features of each operating system shell
+   - Understand the specifics of local login scripts for each shell

# 8.1 Comparison of C, Bourne, Korn, and POSIX Shell Features

Table 8-1 compares selected features of the C shell and the Bourne, Korn, and POSIX shells.

| Feature | Description | C | Bourne | Korn or POSIX |
|---|---|---|---|---|
| Shell programming | A programming language that includes features such as loops, condition statements, and variables. | Yes | Yes | Yes |
| Signal trapping | Mechanisms for trapping interruptions and other signals sent by the operating system. | Yes | Yes | Yes |
| Restricted shells | A security feature that provides a controlled shell environment with limited features. | No | Yes | No |
| Command aliases | A feature that lets you abbreviate long command lines or to rename commands. | Yes | No | Yes |
| Command history | A feature that stores commands and lets you edit and reuse them. | Yes | No | Yes |