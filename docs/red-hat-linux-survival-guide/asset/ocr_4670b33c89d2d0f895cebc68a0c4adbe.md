of good terminal emulation, which is required for a full-screen menu application. Also, note that make menuconfig is not the fanciest way to configure a kernel. That title goes to the make xconfig script, which is described in the next section.

# Configuring the kernel using make xconfig

As you may have guessed from the script name, make xconfig requires the X Window System. On systems with X installed, this is the preferred method of kernel configuration. Figure 11-2 shows the Linux Kernel Configuration window, which appears when the make xconfig script is run from a GUI that's running X.

![](bbox=[0.1, 0.44, 0.95, 0.66])

Figure 11-2 The Linux Kernel Configuration window.

You can click any button to open a dialog box where you can configure a particular section of the entire configuration. For example, Figure 11-3 shows the Processor type and features dialog box.

As you can see, this is quite a user-friendly interface. Another advantage of this interface is that you can open multiple sections by clicking the appropriate buttons. For example, if you are configuring the Partitions Type section and want to confirm that you have enabled UFS file system support in the Filesystems section, you can click the buttons for these two sections and verify your selections.