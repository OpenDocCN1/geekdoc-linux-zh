# Chapter 5 • The Hacking Top 10

# Figure 5.12 Metasploit

![](bbox=[0.087, 0.093, 0.872, 0.506])

Now you are aware that MSF has a GUI that you can run locally with Ruby, which is fine and dandy if you are performing forensics on a single system, which most likely is the workstation of the bad guy, and here is why. To run the GUI, you have to have Ruby installed and running. This takes up a big chunk of memory, and would stand out like a thumb on any business system, as can be seen from the results of a “top” command on my Ubuntu box. The Ruby process is taking up 6.4 percent of the memory, which may not seem like a whole lot, but look at it in comparison to the rest of the processes. Nothing is over .03 percent, which by way of comparison, is 213 times larger than the next largest process.

www.syngress.com