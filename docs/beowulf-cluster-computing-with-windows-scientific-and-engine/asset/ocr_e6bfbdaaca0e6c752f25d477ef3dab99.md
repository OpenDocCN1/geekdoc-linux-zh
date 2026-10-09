POSIX and OS/2 subsystems call services in the Win32 subsystem to perform display I/O. (In fact, if you examine the subsystem type for these images, you’ll see that they are Win32 executables.)

Let’s take a closer look at each of the environment subsystems.

# **Win32 Subsystem.**

The Win32 subsystem consists of the following major components:

+   - The environment subsystem process (csrss.exe) contains support for
+     - console (text) windows,
+     - creating and deleting processes and threads,
+     - portions of the support for 16-bit virtual DOS machine (VDM) processes, and
+     - other miscellaneous functions, such as GetTempFile DefineDosDevice, ExitWindowsEx, and several natural language support functions.

+   - The kernel-mode device driver (win32k.sys) contains two components:
+     - The window manager, which controls window displays; manages screen output; collects input from keyboard, mouse, and other devices; and passes user messages to applications.
+     - The Graphics Device Interface (GDI), which is a library of functions for graphics output devices. It includes functions for line, text, and figure drawing and for graphics manipulation.

+   - Subsystem DLLs (such as Kernel32.dll, Advapi32.dll, User32.dll, and Gdi32.dll) translate documented Win32 API functions into the appropriate undocumented kernel-mode system service calls to Ntoskrnl.exe and Win32k.sys.

+   - Graphics device drivers are hardware-dependent graphics display drivers, printer drivers, and video miniprint drivers.

Applications call the standard USER functions to create user interface controls, such as windows and buttons, on the display. The window manager communicates these requests to the GDI, which passes them to the graphics device drivers, where they are formatted for the display device. A display driver is paired with a video miniprint driver to complete video display support.

The GDI provides a set of standard two-dimensional functions that let applications communicate with graphics devices without knowing anything about the devices. GDI functions mediate between applications and graphics devices such as display drivers and printer drivers. The GDI interprets application requests for graphic output and sends the requests to graphics display drivers. It also provides a standard interface for applications to use varying graphics output devices. This interface enables application code to be independent of the hardware devices and