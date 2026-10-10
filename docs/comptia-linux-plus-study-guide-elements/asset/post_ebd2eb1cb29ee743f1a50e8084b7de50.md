
want to find the recipients of e-mail processed by your mail server. A typical entry might resemble the following:

```
Apr 2 23:52:45 nessus postfix/smtp[30147]: C4F1E6CDE:  
to=<jennie@luna.edu>, relay=smtp.abigsp.com[68.1.17.4]:25, delay=0.56, 
delay=0.02/0.04/0.23/0.27, dsn=2.0.0, status=sent (250 2.0.0 
ars1Lb00l3cX0xk02rs1Gy mail accepted for delivery)
```

The recipient information begins with the string `to=`, so you can use `grep` to locate such lines, eliminating other lines from the input that will be piped into `awk`. You can then use `awk` to isolate the seventh space-delimited field—the one with the recipient information. This is the command to do all of this:

```
$ grep "to=" /var/log/mail.log | awk '{./, {print $7}}'
```

You might need to adjust this command for your system's log file name and the format of its entries. The output will be a series of lines, such as the following:

to=<jennie@luna.edu>,
to=<franklin@example.com>,

The `sed` command more directly modifies the contents of files. Its syntax, like `awk`'s, can take one of two forms:

```
sed [options] -f script-file [input-file]
sed [options] script-text [input-file]
```

In either case, *input-file* is the name of the file you want to modify. (Modifications are actually temporary unless you save them in some way.) The script (*script-text* or the contents of *script-file*) is the set of commands you want `sed` to perform. When passing a script directly on the command line, *script-text* is typically enclosed in single quote marks. Table 4.4 summarizes a few `sed` commands that can be used in its scripts.

### TABLE 4.4 Common sed Commands

| Command | Meaning |
| :--- | :--- |
| = | Display the current line number |
| a\text | Append text to the file |
| i\text | Insert text into the file |
| r filename | Append text from filename into the file |
| s/regex/replacement | Replace text that matches the regular expression (regex) with replacement |

Table 4.4 is incomplete; sed (like awk) is quite complex, and this section merely introduces it.

You can use sed to further clean up the output of the preceding grep/awk command. For instance, if you want only the e-mail address and not the to= string and surrounding punctuation, you could use the following command:

```
$ grep "to=" /var/log/mail.log | awk '/.*/ {print $7} | sed {s/to=<>///}\nsed [s/^>\,///]
```

The backslash character (\) is used to signify that the following character should be interpreted as a literal part of the regular expression rather than as a special control character.

The result of the preceding command will be a series of e-mail addresses, one to a line, as in:

- jennie@luna.edu
- frank@example.com

Although they’re conceptually simple, both sed and awk are very complex tools; even a modest summary of their capabilities would fill a chapter. You can consult their man pages for basic information, but to fully understand these tools, you may want to consult a book on the subject, such as Dale Dougherty and Arnold Robbins’ sed & awk, 2nd Edition (O’Reilly, 1997).

## Using Additional Log File Analysis Tools

Manually examining log files with tail, less, and similar tools can be informative, but other tools exist to help you analyze your log files. One of these is Logcheck, which is part of the Sentry Tools package (http://sourceforge.net/projects/sentrytools/). This package comes with some distributions, such as Debian. Unfortunately, it requires a fair amount of customization for your own system, so it’s most easily implemented if it comes with your distribution, preconfigured for its log file format. If you want to use it on another distribution, you must edit the logcheck.sh file that’s at the heart of the package. This file calls the logtail utility that checks log file contents, so you must configure the script to check the log files you want monitored. You can also adjust features such as the user who’s to receive violation reports and the locations of files that contain strings for which the utility should look in log files. Once it’s configured, you call logcheck.sh in a cron job. Logcheck then e-mails a report concerning any suspicious system logs to the user defined in logcheck.sh (root, by default).

## Summary

System services are those programs that run behind the scenes on any Linux system. Many system services are network server programs, but others are purely local in action. Knowing how to start and stop system services, both on a temporary and a permanent basis, will give you control over how your computer behaves—what network servers it provides to the world, what local utilities it runs, and so on. Most system services are run via SysV startup scripts or via a super server, but you may also use local startup scripts to do the job.

Because system services don't attach themselves to a console, they don't normally display messages for you on your screen. Instead, they write messages to log files. These messages can include warnings about security violations, complaints about unexpected events, and more routine data about normal operations. Knowing how to examine and search log files will enable you to keep an eye on your system’s activity, both to verify normal functioning and to investigate problems—with any luck before they become serious!

## Exam Essentials

- **Describe the SysV startup procedure.** The init process reads the /etc/inittab file or the contents of the /etc/event.d directory, which controls programs that run when changing from one runlevel to another. Scripts in directories corresponding to each runlevel (typically /etc/rc#.d or /etc/rc.d/rc#.d, where # is the runlevel number) start and stop services when the runlevel changes.
- **Explain the differences between SysV startup scripts and super servers for running servers.** SysV startup scripts start servers running on a computer at startup or when changing runlevels so that the servers are always running and can respond quickly to requests, but servers run in this way consume RAM at all times. Super servers run the target servers only in response to requests from clients, thus reducing the memory burden for infrequently used servers but at the cost of slower responses to incoming requests.
- **Summarize how TCP Wrappers or xinetd can improve security.** These programs both perform initial security checks on a connection, such as verifying that the IP address of a client system is authorized to use the server. Only when a client passes any initial checks is the server program launched and the connection handed off to the server program.
- **Describe the function of the runlevel.** Sometimes you may want to run a Linux system with a different set of services than you run at other times. The runlevel lets you define several sets of services and switch quickly between them.
- **Describe the function of a system logger.** A system logger is a daemon that accepts information from servers and other programs that want to record information about their normal operation in standardized log files. The system logger creates and manages these files on behalf of the programs that generate the log entries.
- **Explain why using a remote system logger can be beneficial.** A remote system logger is a computer that accepts log entries for other systems. This practice improves overall network security because it protects logs from tampering by intruders—to change a log file, the intruder must compromise two computers rather than one. You can also search consolidated log files much more easily than you can search them on multiple computers.
- **Summarize how `tail` and `less` differ as tools for examining log files.** The `tail` command displays the final few lines of a file, which is handy if you know an entry you want to see is at the very end of a log file. The `less` command enables you to page through a file, search its contents, and so on. It's not as convenient as `tail` if you just want to see the last few lines of a file, but it's superior if you need to search for information or aren't sure precisely how many lines you need to examine.
