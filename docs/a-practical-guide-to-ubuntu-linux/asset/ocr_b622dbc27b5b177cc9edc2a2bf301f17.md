# TEXTUAL SYSTEM ADMINISTRATION UTILITIES 455

information. Be sure to describe the problem accurately and identify the system carefully. Include information about the version of Ubuntu running on the system and any software packages and hardware that you think relate to the problem. The newsgroup comp.os.linux.answers contains postings of solutions to common problems and periodic postings of the most-to-date versions of FAQs and HOWTO documents. You can also refer to Ubuntu mailing lists (lists.ubuntu.com), the Ubuntu forum (ubuntuforums.org), system documentation (help.ubuntu.com), community documentation (help.ubuntu.com/community), and IRC support (#Ubuntu on irc.freenode.net). You can see www.catb.org/~rs/faqs/smart-questions.html for a helpful paper by Eric S. Raymond and Rick Mieten “How to Ask Questions the Smart Way.”

# TEXTUAL SYSTEM ADMINISTRATION UTILITIES

Many tools can help you be an efficient and thorough system administrator. This section describes a few textual (command-line) tools and utilities; others are described throughout Part IV of this book.

# kill: Sends A SIGNAL TO A PROCESS

The kill builtin sends a signal to a process. This signal may or not terminate (kill) the process, depending on signal it is and how the process is designed. Refer to “trap: Catches a Signal” on page 109 for a discussion of the various signals and their interaction with a process. Running kill is definitely the first method to use when a process needs to be aborted.

Usually a user can kill a process by working in another window or by logging in another terminal. Sometimes, you may have to use sudo to kill a process for a user. To kill a process, you need to know its PID. The ps utility can provide this information once you determine the name of the program the user is running and/or the username of the user. The top utility can also be helpful in finding and killing a runaway process (use the top k command).

kill: Use the kill signal (-KILL or –9) as a method of last resort

caution When you need to use kill, use the termination signal (kill -TERM or kill -15). Only if that tactic does not work should you attempt to use the kill signal (kill -KILL or kill –9).

Because of its inherent dangers, using a kill signal is a method of last resort, especially when you are working with root privileges. One kill command issued while working with root privileges can bring the system down without warning.

In the following example, Sam complains that gnome-calculator is stuck and that he cannot do anything from the gnome-calculator window—not even close it. A more experienced user could open another window and kill the process, but in this case