# CHAPTER 10 | Kernel Risk Mitigation

# 295

![](bbox=[0.045, 0.065, 0.955, 0.335])

# Start the Kernel Customization Process

Navigate to the kernel source code. From this directory, there are several methods for customizing a Linux kernel before it's compiled. You could open the aforementioned config file in a text editor and change settings in that file. That option is considered impractical for all but the most knowledgegable Linux developers. Alternatively, you could run the make config command. It's a simple script. As shown in Figure 10-2, it prompts you to make choices for each option associated with the Linux kernel.

While the questions are straightforward, there are literally thousands of options associated with the Linux kernel. If you miss an option to be changed, you'd have to press Ctrl+C to abort and run the make config command to start over. That makes it impractical to customize the kernel with the make config command.

The practical method for customizing a kernel without a GUI uses ncurses-based configuration menus. In the directory with the kernel source code, run the make menuconfig command. You should see a menu similar to that shown in Figure 10-3.

As the functionality of the Linux kernel evolves, some of the options in the kernel configuration will vary. However, most of the options described in the sections that follow are relatively stable.

# Kernel Configuration Options

Even if you choose to reconfigure a kernel, explore the available options. An understanding of these options can help you understand the strengths and weaknesses of the Linux kernel, including in the area of security.

The options described in the sections that are based on the kernel configuration menu associated with the stock version of the Linux kernel, version 2.6.33, as released by the Linux Kernel Organization. The wording associated with some menu options may

![](bbox=[0.945, 0.795, 0.995, 0.955])