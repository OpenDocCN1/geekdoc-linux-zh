

## A Program Always Crashes

If you have a program that keeps crashing, try running it in a Terminal to see what’s going wrong. You’ll have to get the name of the command needed to run the program first—see "Reporting a Bug" on page 359 for information on how you can find it. Once you have the command, type it into the Terminal, and press ENTER. The program should run as normal, so keep using it until it crashes. When it does, look at the Terminal to see whether it left any clues as to what’s going wrong in there. Error messages in the Terminal can be quite cryptic, so you might like to ask someone on the forums or IRC (both of which are discussed in Chapter 20) if they know what it means.

If the messages in the Terminal are no help, you should report a bug. See "Bugs, Bugs, Glorious Bugs" on page 358 for details.

## A Program Won’t Start

If a program doesn’t start when you click its shortcut in the Applications menu, try running it in the Terminal, as described in the previous section. It could be crashing soon after starting and might leave some information about the crash in the Terminal.

## My Computer Is Running Slowly

Certain tasks take up lots of computing power and cause your computer to run slowly. Burning a CD, installing software, and converting music files to a different format all tend to strain your system, so you shouldn’t be surprised if things feel a little sluggish when something like that is running. But what if your computer is running slowly even if you’re not running anything intensive? You can investigate the cause of the slowdown by selecting System ▸ Administration ▸ System Monitor to open the System Monitor. Select the Resources tab, and check your CPU (processor) usage—if it’s around 100 percent, then a program running in the background is probably responsible for the problem (for example, the one in Figure 21-14). Choose the Processes tab, and click the % CPU column heading a couple of times until it has an "up" arrow next to it. This will sort the list of programs in order of how much of the processor they are using. The one that’s using all of the CPU should appear at the top of the list.

It’s normally best to wait a few minutes and see whether the program reduces its CPU usage by itself. After all, it could be some system software running a scan or some other maintenance operation. If it doesn’t go away, the program might have gotten stuck, so select it and click End Process to force it to close. Your system should return to its usual speed within a few seconds.

If you didn’t notice high CPU usage on the Resources tab, then it’s possible that something is overusing your hard disk instead. Programs that do this almost always finish what they’re doing within five or ten minutes, so you should probably ride it out. If it persists, the easiest way of fixing the problem is by restarting the computer.

![](img/f7cef0df22f9dba5a41777808c98eece_439_0.png)

Figure 21-14: The System Monitor, showing the gwibber-service program using an unhealthy 89 percent of the processor

## Lost Files

Losing an important file is one of those uniquely frustrating experiences in life. If you’ve looked in all of the most likely locations (like your home folder), try one of the following:

- **Recent Documents:** Select Places ▸ Recent Documents to see whether the missing file is in the list of recently edited files. If it was an office document, try the File ▸ Recent Documents menu in OpenOffice.org too.
- **Basic search:** The basic Search for Files tool is useful only if you can remember part of the file’s name. Select Places ▸ Search, type part of the file’s name in the Name contains box, and click Search. It might turn up in the list of search results.
- **Heavy-duty search:** The more advanced Tracker search tool can look inside documents, which is handy if you don’t remember the file’s name but you do remember some of its contents. Install the Tracker Search Tool from the Ubuntu Software Center, and select System ▸ Preferences ▸ Search and Indexing. Check the Enable indexing option on the General tab, and click Apply. Click Restart in the warning window that appears, and wait for Tracker to build its search index (about 15 to 20 minutes should do it). When it has finished, select Applications ▸ Accessories ▸ Tracker Search Tool, and search for your lost file there.

