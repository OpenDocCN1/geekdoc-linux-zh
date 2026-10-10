# *Debugging embedded software*

+   **Chapter Outline**
+   **Remote Debugging With Eclipse** 121
+       Remote Debug Launch Configuration 123
+   **A Thermostat** 126
+   **Host Workstation as Debug Environment** 127
+       Advanced Breakpoint Features 129
+   **Debugger Services Framework** 132
+       Configuring Remote System Explorer 132
+       Debugging With Remote System Explorer 135
+   **Resources** 137

> *If debugging is the process of removing bugs, then programming must be the process of putting them in.*
> *Edsger W. Dijkstra*

In Chapter 5, Eclipse integrated development environment you saw how Eclipse integrates very nicely with the Gnu Debugger, GDB. In this chapter, we will look at additional features of GDB, and explore how to use GDB on our target board. We will also consider a simple approach to high-level simulation that can be useful in the early stages of development.

# *Remote Debugging With Eclipse*

In a typical desktop environment, the target program runs on the same machine as the debugger. But in our embedded environment, Eclipse with GDB runs on the host workstation and the program being debugged runs on the ARM target. You can think of GDB as having both a client and a server side, as illustrated in Fig. 8.1. The client is the user interface, and the server is the actual interaction with the program under test. GDB implements a serial protocol that allows the server and client sides to be separated and communicate either over an RS-232 link or Ethernet.