The disadvantage is that at some point the log file will consume all available disk space. Therefore, you should have multiple log files, with your program switching to a new one periodically.

Brian Kernighan recommends naming the log files by day of the week: myapp.log.sun, myapp.log.mon, and so on. The advantage here is that you don’t have to manually move old files out of the way; you get a week’s worth of log files for free.

+   - Write to a log file only if it already exists. When your program starts up, if the log file exists, it writes information to the log. Otherwise, it doesn’t. To enable logging, first create an empty log file.

+   - Use a fixed-format for messages, one that can be easily parsed by scripting languages such as awk or Perl, for summary and report generation.

+   - Alternatively, generate some form of XML, which is self-describing, and possibly convertible to other formats. (We’re not big fans of XML, but you shouldn’t let that stop you.)

+   - Use syslog() to do logging; the final disposition of logging messages can be controlled by the system administrator. (syslog() is a fairly advanced interface; see the syslog(3) manpage.)

Choosing how to log information is, of course, the easy part. The hard part is choosing what to log. As with all parts of program development, it pays to think before you code. Log information about critical variables. Check their values to make sure they’re in range or are otherwise what you expect. Log exceptional conditions; if something occurs that shouldn’t, log it, and if possible, keep going.

The key is to log only the information you need to track down problems, no more and no less.

# 15.4.2.4 Runtime Debugging Files

In a previous life, we worked for a startup company with binary executables of the product installed at customer sites. It wasn’t possible to attach a debugger to a running copy of the program or to run it from a debugger on the customer’s system. The main component of the product was not started directly from a command line, but indirectly, through shell scripts that did considerable initial setup.