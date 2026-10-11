Memory (1 GB) starts out with minimal usage, but as the day goes along, more and more memory starts getting used up. A frequent question on various Linux mailing lists concerns the usage of memory: “I have 512 MB of RAM and Linux is using almost all of it! What is wrong?” The answer is that nothing is wrong! Linux is doing what it is supposed to—taking advantage of the memory it can access to cache programs and data. It’s not leaking memory due to poorly behaved programs, or being wasted on unnecessary tasks. If you’re still unconvinced, look at it from the opposite point of view. Suppose you had a ton of memory in your computer, but your operating system and applications hardly used any of it. What would have been the point of buying all that memory? It would be like buying an 18,000-square-foot mansion but using only one 250-square-foot room.

The third monitor I keep open watches the network traffic. It’s interesting to see when network traffic spikes—and occasionally serves to remind me that a slow file save or other seemingly pokey operation looks simply be due to a lot of traffic over the wire all of a sudden.

The fourth monitor looks at swap-space usage, and with 1 GB of memory, swap space is hardly ever used. I’ll probably turn that monitor off in a bit, because it’s not providing useful information any longer.

At the bottom of the System Monitor Preferences dialog, you can choose which colors you want to use in each monitor. The default values of those colors are so close to each other that I spent a bit of time tweaking them so they’d be more differentiated.

Once you’ve configured the System Monitor, you’ll want to use it. You can hold your mouse cursor over a monitor and it’ll give you a tooltip that describes the current load of the resources being monitored. For example, holding the mouse over the Memory monitor results in a “Memory: 100% in use” tooltip, as shown in Figure 34.

Right-clicking the System Monitor applet and selecting Open System Monitor gives you more information about the various resources. The Process Listing tab, as shown in Figure 35, shows you a list of all processes, together with the user, the memory the process is taking, the CPU load, and the process ID.

You can change which processes are displayed by using the View drop-down list in the upper right corner of the dialog.

Because you could have a lot of processes running on your machine, note that you can expand the window vertically in order to show as many processes as you desire. Also note that you can use the arrows on the left side of the primary processes to expand or contract subprocesses for certain items. For example, The GIMP has subprocesses for script-fu—if you don’t want to see that information, click on the arrow and the script-fu line will be rolled up.

![](bbox=[0.08, 0.75, 0.28, 0.84])

Figure 34. The System Monitor applets each have tooltips that provide a quick summary of resource usage.