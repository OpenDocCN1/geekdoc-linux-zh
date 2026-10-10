Calendar
X11
Database
People
Mail
Slides
Projects
Personal
Bitmaps
Src
Memos

However, most versions of /ls format output like this:

mail calendar people slides
X11 database personal src
bin doc projects txt
bitmaps memos scripts

Listing the files in neat columns seems like a sensible thing to do, at first. But now /ls contains code that does column formatting, a task that has little to do with listing the contents of a directory. Column formatting can be simple or complex, depending on the environment in which it is used. For example, /ls assumes that the user is using an old-style character terminal 80 characters wide. What happens to the columns when invoking /ls on, say, a window system in which the terminal window is 132 characters wide? Suppose the user would prefer to view the output in two columns instead of four? What if the terminal uses a variable-width character set? Suppose the user would prefer to follow every fifth line of file names with a solid line? The list goes on.

In all fairness, /ls retains the ability to list the contents of a directory one file per line. That is about all it should do, leaving the column work to other commands better suited to formatting tasks. /ls would then be a much smaller command (i.e., easier to understand, easier to maintain, using fewer system resources, and so on).

Since writing an application that does one thing well results in a smaller program, these two tenets complement each other. Small programs tend to be unifunctional. Unifunctional programs tend to be small.

A hidden benefit of this approach is that you remain focused on the current task, distilling it to the essence of what you're trying to accomplish. If you cannot make the program do one thing well, then you probably don't comprehend the problem you're trying to solve. In a later chapter, we'll discuss how to acquire that understanding the Unix way. For now, think small.