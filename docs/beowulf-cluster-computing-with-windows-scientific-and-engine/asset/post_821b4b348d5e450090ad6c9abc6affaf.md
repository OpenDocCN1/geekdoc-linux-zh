
![](img/e2283ffaea56e577ac05056b4bb738fc_303_0.png)

# **Figure 11.4**

Snapshot of XPVM interface during use

all running PVM tasks, shuts down PVM cleanly, and exits the XPVM interface. The *Help* button brings up a menu of topics for which information is available. While an application is running, XPVM collects and displays the information in real time. Although XPVM updates the views as fast as it can, there are cases when XPVM cannot keep up with the events and falls behind the actual run time.

In the middle of the XPVM interface are tracefile controls. Here you can specify a tracefile; a default tracefile in \pvm\t is initially displayed. There are buttons to specify whether the specified tracefile is to be played back or overwritten by a new run. XPVM saves trace events in a file using the “self-defining data format” (SDDF) described in Dan Reed’s Pablo trace displaying package (other packages such as Pablo can be used to analyze the PVM traces).

XPVM can play back its own SDDF files. The tape playerlike buttons allow you to rewind the tracefile, stop the display at any point, and step through the execution. A time display specifies the number of seconds from when the trace display began.

The *Views* button allows you to open or close any of several views presently supplied with XPVM. These views are described below.

During startup, XPVM joins a group called `xpvm`. This is done so tasks that are started outside the XPVM interface can get the tid of XPVM by doing `tid = pvm.gettid( xpvm, 0 )`. This tid would be needed if you wanted to manually turn on tracing inside such a task and pass the events back to XPVM for display. The expected TraceCode for these events is **666**.

# 11.10.1 Network View

The *Network* view displays the present virtual machine configuration and the activity of the hosts. Each host is represented by an icon that includes the `PVM_ARCH` and hostname inside the icon. In the current release of XPVM, the icons are arranged arbitrarily on both sides of a bus network. In future releases the view will be extended to visualize network activity as well. At that time you will be able to specify the network topology to display.

These icons are illumined in different colors to indicate their status in executing PVM tasks. Green implies that at least one task on that host is busy executing useful work. Yellow indicates that no tasks are executing user computation but at least one task is busy executing PVM system routines. When there are no tasks on a given host, its icon is left uncolored or white. The specific colors used in each case are user customizable.

You can tell at a glance how well the virtual machine is being utilized by your PVM application. If all the hosts are green most of the time, then machine utilization is good. The Network view does not display activity due to other users’ PVM jobs or other processes that may be running on the hosts.

In future releases the view will allow you to click on a multiprocessor icon and get information about the number of processors, number of PVM tasks, and the like that are running on the host.

# 11.10.2 Space-Time View

The *Space-time* view displays the activities of individual PVM tasks that are running on the virtual machine. Listed on the left-hand side of the view are the executable names of the tasks preceded by the host they are running on. The task list is sorted by host so that it is easy to see whether tasks are being clumped on one host. This list also shows the task to host mappings (which are not available in the Network view).

The Space-time view combines three different displays. The first is like a Gantt chart. Beside each listed task is a horizontal bar stretching out in the “time” direction. The color of this bar at any time indicates the state of the task. Green indicates that user computations are being executed. Yellow marks the times when the task is executing PVM routines. White indicates when a task is waiting for messages. The bar begins at the time when the task starts executing and ends when the task exits normally. The specific colors used in each case are user customizable.

The second display overlays the first display with the communication activity among tasks. When a message is sent between two tasks, a red line is drawn starting at the sending task’s bar at the time the message is sent and ending at the receiving task’s bar when the message is received. Note that this is not the time the message arrived, but rather the time the task called `pvm_recv()`. Visually, the patterns and slopes of the red lines combined with white “waiting” regions reveal a lot about the communication efficiency of an application.

The third display appears only when you click on interesting features of the Space-time view with the left mouse button. A small “pop-up” window appears, giving detailed information regarding specific task states or messages. If a task bar is clicked on, the state begin and end times are displayed along with the last PVM system call information. If a message line is clicked on, the window displays the send and receive time as well as the number of bytes in the message and the message tag.

When the mouse is moved inside the Space-time view, a blue vertical line tracks the cursor, and the time corresponding to this vertical line is displayed as Query time at the bottom of the display. This vertical line also appears in the other “something vs. time” views so you can correlate a feature in one view with information given in another view.

You can zoom into any area of the Space-time view by dragging the vertical line with the middle mouse button. The view will unzoom back one level when the right mouse button is clicked. Often, very fine communication or waiting states are visible only when the view is magnified with the zoom feature. As with the Query time, the other views also zoom along with the Space-time view.

# 11.10.3 Other Views

XPVM is designed to be extensible. New views can be created and added to the Views menu. At present, there are three other views: Utilization, Call Trace, and Task Output. Unlike the Network and Space-time views, these views are closed by default. Since XPVM attempts to draw the views in real time, the fewer open views the faster XPVM can draw.

The Utilization view shows the number of tasks computing, in overhead, or waiting for each instant. It is a summary of the Space-time view for each instant. Since the number of tasks in a PVM application can change dynamically, the scale on the Utilization view will change dynamically when tasks are added, but not when they exit. When this happens, the displayed portion of the Utilization view is completely redrawn to the new scale.

The Call Trace view provides a textual record of the last PVM call made in each task. The list of tasks is the same as in the Space-time view. As an application runs, the text changes to reflect the most recent activity in each task. This view is useful as a call-level debugger to identify where a PVM program's execution hangs.

XPVM automatically tells all tasks it spawns to redirect their standard output back to XPVM when the Task Output view is opened. This view gives you the option of redirecting the output into a file. If you type a file name in the “Task Output” box, the output is printed in the window and into the file.

As with the trace events, a task started outside XPVM can be programmed to send standard output to XPVM for display by using the options in pvm_setopt(). XPVM expects the OutputCode to be set to 667.

# **12 Fault-Tolerant and Adaptive Programs with PVM**

*Al Geist and Jim Kohl*

The use of Beowulf clusters has expanded rapidly in the past several years. Originally created by researchers to do scientific computing, today these clusters are being used in business and commercial settings where the requirements and expectations are quite different. For example, at a large Web hosting company the reliability and robustness of their applications are often more important than their raw performance.

A number of factors must be considered when you are developing applications for Beowulf clusters. In the preceding chapters the basic methods of message passing were illustrated so that you could create your own parallel programs. This chapter describes the issues and common methods for making parallel programs that are fault tolerant and adaptive.

*Fault tolerance* is the ability of an application to continue to run or make progress even if a hardware or software problem causes a node in the cluster to fail. It is also the ability to tolerate failures within the application itself. For example, one task inside a parallel application may get an error and abort. Because Beowulf clusters are built from commodity components that are designed for the desktop rather than heavy-duty computing, failures of components inside a cluster are higher than in a more expensive multiprocessor system that has an integrated RAS (Reliability, Availability, Serviceability) system.

While fault-tolerant programs can be thought of as adaptive, the term “adaptive programs” is used here more generally to mean parallel (or serial) programs that dynamically change their characteristics to better match the application’s needs and the available resources. Examples include an application that adapts by adding or releasing nodes of the cluster according to its present computational needs and an application that creates and kills tasks based on what the computation needs.

In later chapters you will learn about Condor and other resource management tools that automatically provide some measure of fault tolerance and adaptability to jobs submitted to them. This chapter teaches the basics of how to write such tools yourself.

PVM is based on a dynamic computing model in which cluster nodes can be added and deleted from the computation on the fly and parallel tasks can be spawned or killed during the computation. PVM does not have nearly as rich a set of message-passing features as MPI; but, being a virtual machine model, PVM has a number of features that make it attractive for creating dynamic parallel programs. For this reason, PVM will be used to illustrate the concepts of fault tolerance and adaptability in this chapter.
