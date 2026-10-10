use it to describe any task where some files must be updated automatically from others whenever the others change.
To prepare to use make, you must write a file called the *makefile* that describes the relationships among files in your program, and the states the commands for updating each file. In a program, typically the executable file is updated from object files, which are in turn made by compiling source files.
Once a suitable makefile exists, each time you change some source files, this simple shell command
**make**
suffices to perform all necessary recompilations. The *make* program uses the makefile database and the last-modification times of the files to decide which of the files need to be updated. For each of those files, it issues the commands recorded in the database.
*make* executes commands in the makefile to update one or more target *names*, where *name* is typically a program. If no *-f* option is present, *make* will look for the makefiles *GNUmakefile*, *makefile*, and *Makefile*, in that order.
Normally you should call your makefile either *makefile* or *Makefile*. (We recommend *Makefile* because it appears prominently near the beginning of a directory listing, right near other important files such as *README*.) The first name checked, *GNUmakefile*, is not recommended for most makefiles. You should use this name if you have a makefile that is specific to *GNU make*, and will not be understood by other versions of *make*. If *makefile* is -, the standard input is read.
*make* updates a target if it depends on prerequisite files that have been modified since the target was last modified, or if the target does not exist.

# OPTIONS

+   **-b -m** These options are ignored for compatibility with other versions of *make*.

+   **-C dir** Change to directory *dir* before reading the makefiles or doing anything else. If multiple -C options are specified, each is interpreted relative to the previous one: *-C / -C* etc is equivalent to *-C /etc*. This is typically used with recursive invocations of *make*.

+   **-d** Print debugging information in addition to normal processing. The debugging information says which