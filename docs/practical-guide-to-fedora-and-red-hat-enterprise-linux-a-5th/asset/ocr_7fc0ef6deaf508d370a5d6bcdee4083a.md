![](bbox=[0.2, 0.1, 0.85, 0.43])

# Figure 15-1  The Linux Kernel Configuration window, split view

The make config command displays the Linux Kernel Configuration window. You can view this window in three configurations: single, split, or full view. Choose a view by clicking one of the three icons in the middle of the toolbar. Figure 15-1 shows the split view. In this view, the left frame shows the options and the top-right frame lists the features for each option. The bottom-right frame describes the highlighted option or feature. Figure 15-2 shows the full view.

In the split and full views, click the triangles at the left ends of menu lines to expand or collapse feature menus. A small box appears at the left end of those lines that describe features you can change. An empty box indicates the feature is disabled, a check mark indicates it is to be included in the kernel, and a dash means it is to be compiled as a module. Double-click the box to change the state of the feature.

Go through the features and mark each as you would like it configured in the new kernel. At any time during the configuration process, you can store the currently defined configuration to a file, load a configuration from a file, or exit with or without saving your changes. See the selections in File on the Menubar. When you are done, select Menubar: File\Save and close the window.

# EXTRAVERSION NUMBER

To prevent overwriting existing kernel files and to identify various compilations of the kernel, you can use the EXTRAVERSION variable in Makefile. This variable is initially set to .5 (PEDOR) or -prep (RHEL). Whatever value you assign to this variable is placed at the end of the kernel name and release number to identify the kernel. You can make note of patches applied to the kernel in this string to help people track down problems later on.