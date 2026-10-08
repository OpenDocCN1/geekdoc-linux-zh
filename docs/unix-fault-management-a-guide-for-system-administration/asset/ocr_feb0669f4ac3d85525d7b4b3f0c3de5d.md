# Figure 4-13 Using SyMON dynamic reconfiguration to replace a failed memory board.

![](bbox=[0.14, 0.14, 0.96, 0.44])

offline. In contrast, slot 0 is associated with a permanent memory bank and can’t be disconnected while the system is running.

# Setting Up Monitoring and Reconfiguration

From the Enterprise SyMON console, Bill loads the Config-Reader and Dynamic Reconfiguration modules to ensure that he will be notified of hardware faults, so that he can handle the faults without having to take the system down. The Config-Reader module is located under Hardware and the Dynamic Reconfiguration module is located under local applications (shown in Figure 4-7, earlier in this chapter).

# Memory Board Failure Occurs

When a critical memory fault occurs, the icon for the system on the SyMON console indicates the alarm. Bill looks at the Alarm window to see more details about the event. He notices that a memory board has failed. Using the Logical View, like the one shown in Figure 4-14, he locates the failed memory board. Using the Physical View, like the one shown earlier in Figure 4-5, he locates the exact location of the physical board in the system.

# Fixing the Failure and Restoring Service

Bill accesses the Dynamic Reconfiguration screen from the SyMON console. First, he selects the failed memory slot and clicks the Disconnect button to unconfigure and disconnect the board. Next, he replaces the failed board and then connects the board by clicking the Connect button; he leaves it temporarily unconfigured, however, while he performs a memory test using