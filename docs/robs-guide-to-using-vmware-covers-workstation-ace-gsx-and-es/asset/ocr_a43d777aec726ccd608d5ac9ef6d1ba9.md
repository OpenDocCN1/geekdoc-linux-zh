# Changing snapshot priority

With VMware Workstation, virtual machine snapshots are created and restored as a background process. This is a great feature because you can almost instantaneously continue working with the guest OS while the snapshot process is finishing up. If you try to start a new snapshot process when another one is not finished, you will receive a message about it.

![](bbox=[0.12, 0.29, 0.58, 0.62])

It depends on the usage scenario of the virtual machine whether you want to keep this feature turned on. In a classroom environment for example, students who revert to a snapshot can start working immediately. However, when they do this, the machine might be slow in the beginning. Depending on the audience, it might be better to let them wait until the process is finished as a foreground process.

To change the way that the snapshots are created, select VM → Preferences and enable or disable the checkbox in the Priority tab.

Figure 3.7: Snapshots are created as a background process by default.

# 3.8 Cloning Virtual Machines

This new feature allows you to create a copy of a virtual machine. It is different than using snapshots. With multiple snapshots on a virtual machine only one of the snapshots can be active, whereas you can boot one or more clones that you have created of a virtual machine at the same time.

There are a wide in variety of usage examples for virtual machine clones. For an instructor who has to set up a classroom with virtual machines, this wizard helps him to easily create unique machines for each student. With the linked clone setup, explained later, the parent could reside on the network, while the student's clone machine is on his own computer.

Other uses are for software testing where at any point in time, or even at a given snapshot in a snapshot tree, you need to have someone else work on the same environment to perform tests for you. Clone the virtual machine and provide them with that copy to work on.