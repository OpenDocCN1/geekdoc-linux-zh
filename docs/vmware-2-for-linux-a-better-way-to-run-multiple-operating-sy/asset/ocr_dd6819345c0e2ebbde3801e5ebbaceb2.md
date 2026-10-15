VMware's unique virtual machine design makes it extremely powerful and probably unlike anything you've ever seen before, even if you've experimented with emulators and virtual machines in the past.

This chapter pops open the VMware hood and explains in detail what VMware can do and how it's done.

# Sharing the CPU

The most important thing to remember about VMware's virtual machine design is that your CPU's attention is split between your host OS (Linux) and whatever guest OS you run in VMware. That's because VMware looks just like a Linux application to the Linux task scheduler.

The VMware software layer and Linux's own multitasking kernel manage the CPU demand to ensure that neither side can completely deny the other of attention, although it is possible for heavy demand from either to greatly slow down your computer. Think of a flowing stream, with a new irrigation branch. As long as things remain under control and nobody gets too greedy, there's still plenty of water for everyone. Figure 2.1 is a diagram of the VMware virtual machine architecture.

VMware runs in two pieces: the virtual machine itself, in which your guest operating system and programs run, and a "traffic cop" VMware Virtual Platform software layer

![](bbox=[0.18, 0.71, 0.78, 0.92])

Figure 2.1 A look at VMware's design (permission to use copyrighted graphic granted by VMware, Inc.)