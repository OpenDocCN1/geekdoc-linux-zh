# chapter
13

![](bbox=[0.62, 0.05, 0.92, 0.28])

# The Interactive Bash Shell

# 13.1 Introduction

With an interactive shell, the standard input, output, and error are tied to a terminal. When using the Bourne Again shell (Bash) interactively, you type UNIX/Linux commands at the bash prompt and wait for a response. Bash provides you with a large assortment of built-in commands and command-line shortcuts, such as history, aliases, file and command completion, command-line editing, and many more. Some of the features were present in the standard UNIX Bourne shell and Korn shell, but the GNU project has expanded the shell to include a number of new features as well adding POSIX compliance. With the release of Bash 2.x, so many features of the UNIX Korn shell and C shell have been included that the bash shell is a fully functional shell at both the interactive and programming level, while upwardly compatible with the standard Bourne shell. For UNIX users, bash offers an alternative to the standard shells, sh, csh, and ksh.

This chapter focuses on how you interact with bash at the command line and how to customize your working environment. You will learn how to take advantage of all shortcuts and built-in features in order to create an efficient and fun working environment. Chapter 14 takes you a step further. Then you will be ready to write bash shell scripts to further tailor the working environment for yourself by automating everyday tasks and developing sophisticated scripts, and if you are an administrator, doing the same not only for yourself but also for whole groups of users.

# 13.1.1 Versions of bash

The Bourne Again shell is a Capricorn, born on January 10, 1988, fathered by Brian Fox and later adopted by Chet Ramey, who now officially maintains bash, enhances it, and fixes bugs. The first version of bash was 0.99. The current version (as of this writing) is version 2.05. Major enhancements were completed in version 2.0, but some operating

> 1. Although bash is traditionally the default shell for Linux platforms, it now comes bundled with Solaris 8.