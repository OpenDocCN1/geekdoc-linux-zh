![](bbox=[0.05, 0.17, 0.95, 0.63])

# **Figure 11.4**  

Snapshot of XPVM interface during use

all running PVM tasks, shuts down PVM cleanly, and exits the XPVM interface. The *Help* button brings up a menu of topics for which information is available. While an application is running, XPVM collects and displays the information in real time. Although XPVM updates the views as fast as it can, there are cases when XPVM cannot keep up with the events and falls behind the actual run time.

In the middle of the XPVM interface are tracefile controls. Here you can specify a tracefile; a default tracefile in \pvm\t is initially displayed. There are buttons to specify whether the specified tracefile is to be played back or overwritten by a new run. XPVM saves trace events in a file using the “self-defining data format” (SDDF) described in Dan Reed’s Pablo trace displaying package (other packages such as Pablo can be used to analyze the PVM traces).

XPVM can play back its own SDDF files. The tape playerlike buttons allow you to rewind the tracefile, stop the display at any point, and step through the