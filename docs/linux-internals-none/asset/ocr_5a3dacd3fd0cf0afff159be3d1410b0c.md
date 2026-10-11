# # The net/ Directory

All the code for networking support is in the net/ directory. TCP/IP, Netware, and Appletalk are all in here.

# ## Compiling It

Before you can actually compile the kernel, you must tell the compilation utilities which functionalities you want, and whether to include those functionalities built into the kernel or configured as a dynamically loadable module (we will see later how the kernel handles loadable modules).

Table 2.1 shows the commands used to configure the kernel.

| **Type** | **Command (as root)** |
| :------- | :-------------------- |
| Text prompt | `make config` |
| Text menus (ncurses style) | `make menuconfig` |
| GUI (requires X to run) | `make xconfig` |

+   **TABLE 2.1**
+   Commands used
+   to configure the
+   kernel

As you can see in the table above there are three ways to configure a kernel. The `make config` simply opens a character mode dialog that will ask one question after the other on the terminal until all questions are answered. For each question there are three possible answers: Yes, No or Module. Module here tells the kernel configuration to use a loadable module dynamically at execution time instead of statically linking the function into the kernel. This will somewhat slow down the first calling of the particular function at execution time, it is however compensated by a significantly smaller kernel. If you need to fit your kernel onto a diskette this is often the only way to do it.

`make menuconfig` opens up a colourful (on a color terminal) menu-based utility that will allow you to configure the kernel as needed. Most people use to configure their kernels this for the ease of use it offers. The functionality is obviously the same as with the other two commands.

The third way to configure a kernel, is `make xconfig`. This works only if you have a correctly configured and running X Window environment. It will allow to use the mouse to select items and set them as needed.