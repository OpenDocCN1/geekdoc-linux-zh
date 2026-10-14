The grep command is often used at the end of a pipe, so that grep is searching the output of another command instead of a file. For example, you could pipe the output of the locate command through grep to refine a search. Suppose you want to search among all .tif graphics files on the system for your airframe image, but you can't remember the exact file name you used (perhaps airframe.tif, airframes.tif, old_air_frame.tif, or something similar). You can use a command such as this:

```
$ locate tif | grep frame
```

In cases such as this, grep uses only a single parameter—the pattern to search for. Rather than include a file name to define the text to be searched, the output of the locate command is searched. The results are printed to STDOUT—the screen.

# Examining File Contents

Linux includes many commands to tell you about a file. You have learned about some of these already, such as the file command, which tells you what type of data a file contains. In this section you learn about commands that examine the contents of files in more detail.

The head and tail commands display the first few lines and last few lines of a file, respectively. By default, head prints the first 10 lines of a file, and tail prints the last 10 lines of a file. Both print the output to STDOUT, which you can redirect as needed. To change the number of lines produced as output, add the -n option to either the head or tail command. For example, to output the last 20 lines of a file named README, use this command:

```
$ tail -n 20 README
```

The tail command includes a feature that lets you see lines as they are added to a file. When you use the -f option, tail displays the last 10 lines of the file, but it doesn't return you to a command prompt—instead, it "follows" the file, printing new lines as they are added to the file by other programs. This is very useful for tracking a log file. For example, suppose you are not certain if your USB device is being detected when you plug it in. (A USB device might be a scanner, hard disk, or digital camera, for example.) The system log file, /var/log/messages, displays messages from the Linux kernel as it detects any new devices. So to see if your USB device is being detected, you can enter the following command, then insert your USB device, and watch the screen to see if new messages appear at the end of the file. Figure 5-1 shows example output from this command (your output will vary depending on what is running on your system at the moment).

```
$ tail -f /var/log/messages
```

The messages are written to the file by another program, but the tail command watches for them and writes them to STDOUT. When you want to end the tail command (stop following the file), press Ctrl+C.