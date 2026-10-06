# Command Line control Keys

| CONTROL-C | Is the default interrupt key: It aborts execution of the program you are running (page 38). |
| CONTROL-D, logout, or exit | Logs you off the system from a character-based interface or out of a shell from a GUI interface (page 36). |
| CONTROL-H or BACKSPACE | Is the default erase key: It erases a character on the command line (page 37). |
| CONTROL-R or CONTROL-L | Refreshes the screen. |
| CONTROL-U | Is the default line kill key: It deletes the entire command line (page 38). |
| CONTROL-W | Is the default erase key: It erases a word on the command line (page 38). |
| CONTROL-Z | Is the default suspend key: It stops execution of the command you are running and returns you to the shell. For more information, refer to "bg: Sends a job to a Background" on page 556. |

Once you press RETURN, a program called shell interprets the words of the command. By default, accounts under Red Hat Linux use the Bourne Again Shell (bash), and many users stay with bash. Other shells are available, including the TC Shell (tc) and the Z Shell (zsh). The shells treat many special characters differently from regular characters; when you want to represent one you must quote it. One way to quote a character is to precede it with a backslash (\).

You often use an editor to create a file in the GNU/Linux filesystem. Among the editors available on Red Hat Linux systems are vi, emacs, and pico. Chapters 10 and 11 cover vi and emacs. The pico editor is popular and easy to learn and use. The Help feature provides a short summary of the key sequences for the main editing commands. You can refer to the Help window online when practicing with pico.

The man (or xman) utility is helpful to new GNU/Linux users, as well as experienced users who must delve into the system documentation for information on the fine points of a utility's behavior. The info utility helps the beginner and expert alike. This utility includes a tutorial on its use and documentation on many GNU/Linux utilities.

After reading this chapter and experimenting on your system, you should be comfortable using the utilities listed in the following table. Part III has more information on ls, rm, man, and cat. Appendix B has a list of resources that you can use to obtain more information.