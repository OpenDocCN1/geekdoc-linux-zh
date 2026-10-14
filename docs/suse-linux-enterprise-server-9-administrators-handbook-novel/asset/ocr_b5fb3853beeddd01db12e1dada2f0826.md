# **FIGURE 9.4**

Defining the printer model.

![](bbox=[0.174, 0.157, 0.756, 0.44])

After you choose the appropriate printer model, you are presented with the configuration summary page, shown in Figure 9.5. At this point, clicking the OK button saves the defined configuration into the various files used by CUPS. After the configuration is saved, the printer will become available to all the system's users. We explore the fine-tuning of queue restrictions later in this chapter. First, though, let's look at how defining a network-based printer is different.

# Adding a Network Printer

In YaST, adding a queue definition on a local server for a network printer is almost identical to setting up a local printer. The main difference encountered in selecting a network-based printer in Figure 9.2 is that the local interface selection option is replaced with a network configuration screen. For an SMB queue, you are presented with a window similar to that shown in Figure 9.6.

> **NOTE**
> 
> A workgroup is a collection of machines in a Windows/Samba environment. When a system is configured, it can be placed within a specific workgroup. When you are searching the network for computers, only systems in the same workgroup will be discovered. This permits the segregation of machines based on function.