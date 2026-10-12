# Understanding Performance Measurement Techniques

We have discussed performance considerations, costs, and benefits, but how does it actually get done? There is always a bottleneck somewhere. But there is a point that can be reached where the bottleneck is not apparent to the user because it is actually small compared to one you may have just gotten rid of. Here is a good example: The Linux server Larry has some sort of obvious memory bottleneck. Larry needs more memory and complimentary swap space. Being the wise administrator you are, you planned for this. You add memory to Larry and summarily increase swap space. Larry now appears to be running just fine. In your day-to-day monitoring of Larry, you notice that the disk I/O is now the bottleneck, but the system appears to be running just fine. This is where bottleneck masking comes into play. In this case it is acceptable, but sometimes you may discover that there is another problematic (or soon to be) bottleneck that was hidden because of a more urgent and pressing performance issue.

There are a wide variety of tools both inherent and off-the-shelf for performance monitoring. For the sake of simplicity (and perhaps reality), this section focuses on tools that come with Linux systems. First, we will examine console-based tools, then move onto some X-tools that are available with most distributions of Linux. Finally, we will look at tools that may or may not be included with common distributions but are easily downloaded and usable under a variety of X Windows environments.

# Console-Based Tools

On most UNIX systems (Linux being no exception), an administrator’s most common performance monitoring tools are console-based tools, or rather tools that operate from the command line. The main reason for this is remote access. An administrator can telnet in from home or across a network and quickly assess what is happening and how to fix it. Another reason for this is that console-based tools tend not to create as much of a load on a system as X Windows-based tools.

# Process Monitoring with top

Arguably one of the most-used console performance monitoring tools to date is top, which, by definition, displays the top CPU-intensive processes in real time. The top display is refreshed every five seconds by default, but can be modified with the -s option for longer or shorter intervals. Top also provides an interactive interface for modifying processes. Following is the syntax for starting top in default mode:

```
$ top
```