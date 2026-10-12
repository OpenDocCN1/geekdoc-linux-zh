
An 8MB query cache should be enough for most people, but larger sites might want 16MB or even 32MB if you are storing a particularly large amount of data. Very few sites will have need to go beyond a 32MB query cache, but keep an eye on the Qcache_lowmem_prunes value to ensure you have enough RAM allocated.

Using the query cache does not incur much of a performance hit. When MySQL calculates the result of a query normally, it simply throws it away when the connection closes. With the query cache, it skips the throwing away, and so there is no extra work being done. If your site does have many updates and deletes, be sure to check whether you get any speed boost at all from the query cache.

## Miscellaneous Tweaks

If you have tuned your key buffer and optimized your query cache and yet still find your site struggling, there are a handful more smaller changes you make that will add some more speed.

When reading from tables, MySQL has to open the file that stores the table data. How many files it keeps open at a time is defined by the table_cache setting, which is set to 64 by default. You can increase this setting if you have more than 64 tables, but you should be aware that Fedora does impose limits on MySQL about how many files it can have open at a time. Going beyond 256 is not recommended unless you have a particularly DB-heavy site and know exactly what you are doing.

The other thing you can tweak is the size of the read buffer, which is controlled by read_buffer_size and read_buffer_rnd_size. Both of these are allocated per connection, which means you should be very careful to have large numbers. Whatever you choose, read_buffer_rnd_size should be three to four times the size of read_buffer_size, so if read_buffer_size is 1MB (suitable for very large databases), read_buffer_rnd_size should be 4MB.

## Query Optimization

The biggest speed-ups can be seen by reprogramming your SQL statements so they are more efficient. If you follow these tips, your server will thank you:

- Select as little data as possible. Rather than SELECT *, select only the fields you need.
- If you only need a few fields, use LIMIT to select the number you need.
- Declare fields as NOT NULL when creating tables to save space and increase speed.
- Provide default values for fields, and use them where you can.
- Be very careful with table joins because they are the easiest way to write inefficient queries.
- If you must use joins, be sure you join on fields that are indexed.
- Find and fix slow queries. Add `log-long-format` and `log-slow-queries = /var/log/slow-queries.log` to your `/etc/my.cnf` file, under `[mysqld]`, and MySQL will tell you the queries that took a long time to complete.
- Use `OPTIMIZE TABLE tablename` to defragment tables and refresh the indexes.

## Reference

http://www.coker.com.au/bonnie++/—The home page of bonnie, a disk benchmarking tool. It also contains a link to RAID benchmarking utilities and Postal, a benchmarking utility for SMTP servers.

http://httpd.apache.org/docs-2.0/misc/perf-tuning.html—The official Apache guide to tuning your web server.

http://dev.mysql.com/doc/mysql/en/mysql-optimization.html—Learn how to optimize your MySQL server direct from the source, the MySQL manual.

There is one particular MySQL optimization book that will really help you get more from your system if you run a large site, and that is *High Performance MySQL* by Jeremy Zawodny and Derek Balling (O’Reilly), ISBN: 0-596-00306-4.

# CHAPTER 35 Command-line Masterclass

In the earlier years of Linux, people made a big fuss of the graphical environments that were available—they rushed to tell new users that you really did not need to keep going back to the command line to type things. Now Linux is more mature, people accept that the command line is still a reality, and a welcome one. While the GUI does indeed make life easier for day-to-day tasks, your options are limited by what the developers wanted you to have—you cannot bring commands together in new ways, and neither can you use any of the GUI features if, for example, your GUI is broken. It does happen!

In his book *The Art of Unix Programming*, Eric Raymond wrote a short story that perfectly illustrates the power of the command line versus the GUI. It’s reprinted here with permission, for your reading pleasure:

One evening, Master Foo and Nubi attended a gathering of programmers who had met to learn from each other. One of the programmers asked Nubi to what school he and his master belonged. Upon being told they were followers of the Great Way of Unix, the programmer grew scornful.

“The command-line tools of Unix are crude and backward,” he scoffed. “Modern, properly designed operating systems do everything through a graphical user interface.”

Master Foo said nothing, but pointed at the moon. A nearby dog began to bark at the master’s hand.

“I don’t understand you!” said the programmer.

> Raymond, Eric. *The Art of Unix Programming*. Addison-Wesley, 2004.

## IN THIS CHAPTER

- Why Use the Shell?
- Basic Commands
- Combining Commands Together
- Multiple Terminals
- Reference

Master Foo remained silent, and pointed at an image of the Buddha. Then he pointed at a window. “What are you trying to tell me?” asked the programmer.

Master Foo pointed at the programmer’s head. Then he pointed at a rock.

“Why can’t you make yourself clear?” demanded the programmer.

Master Foo frowned thoughtfully, tapped the programmer twice on the nose, and dropped him in a nearby trash can.

As the programmer was attempting to extricate himself from the garbage, the dog wandered over and piddled on him.

At that moment, the programmer achieved enlightenment.

Whimsical as the story is, it does illustrate that there are some things that the GUI just does not do well. Enter the command line: It is a powerful and flexible operating environment on Linux, and—if you practice—can actually be quite fun, too!

In this chapter, you will learn how to master the command line so that you are able to perform common tasks through it, and also link commands together to create new command groups. We will also be looking at the two most popular Linux text editors: Vim and Emacs. The command line is also known as the shell, the console, the command prompt, and the CLI (command-line interpreter). For the purposes of this chapter these are interchangeable, although there are fine-grained differences between them!

## Why Use the Shell?

Moving from the GUI to the command line is a conscious choice for most people, although it is increasingly rare that it is an either/or choice. While in X, you can press Ctrl+Alt+F1 at any time to switch to a terminal, but most people tend to run an X terminal application that allows them to have the point-and-click applications and the command-line applications side by side.

Reasons for running the shell include:

- You want to chain two or more commands together.
- You want to use a command or parameter available only on the shell.
- You are working on a text-only system.
- You have used it for a long time and feel comfortable there.

Chaining two or more commands together is what gives the shell its real power. Hundreds of commands are available and, by combining them in different ways, you get hundreds of new commands. Some of the shell commands are available through the GUI, but these commands usually have only a small subset of their parameters available, which limits what you are able to do with them.

Working from a text-only system encapsulates both working locally with a broken GUI and also connecting to a remote, text-only system. If your Linux server is experiencing problems, the last thing you want to do is load it down with a GUI connection-working in text mode is faster and more efficient.

The last use is the most common: People use the shell just because it is familiar to them, with many people even using the shell to start GUI applications just because it saves them taking their hands off the keyboard for a moment! This is not a bad thing; it provides fluency and ease with the system and is a perfectly valid way of working.

## Basic Commands

It is impossible to know how many commands the average shell citizen uses, but if we had to guess, we would place it at about 25:

- cat—Prints the contents of a file
- cd—Changes directories
- chmod—Changes file access permissions
- cp—Copies files
- du—Prints disk usage
- emacs—Text editor
- find—Finds files by searching
- gcc—The C/C++/Fortran compiler
- grep—Searches for a string in input
- less—Filter for paging through output
- ln—Creates links between files
- locate—Finds files from an index
- ls—Lists files in the current directory
- make—Compiles and installs programs
- man—The manual page reader
- mkdir—Makes directories
- mv—Moves files
- ps—Lists processes
- rm—Deletes files and directories
- ssh—Connects to other machines
- tail—Prints the last lines of a file
- top—Prints resource usage
- vim—A text editor
