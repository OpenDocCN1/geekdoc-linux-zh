
## Windows 2000 系统架构组件

- The **Windows 2000 _executive_** contains the base operating system services, such as memory management, process and thread management, security, I/O, and interprocess communication.

- The **Windows 2000 _kernel_** consists of low-level operating system functions, such as thread scheduling, interrupt and exception dispatching, and multiprocessor synchronization. It also provides a set of routines and basic objects that the rest of the executive uses to implement higher-level constructs.

- **_Device drivers_** include hardware device drivers that translate user I/O function calls into specific hardware device I/O requests, as well as file system and network drivers.

- The **_hardware abstraction layer_** is a layer of code that isolates the kernel, device drivers, and the rest of the Windows 2000 executive from platform-specific hardware differences (such as differences between motherboards).

- The **_windowing and graphics system_** implements the graphical user interface (GUI) functions (better known as the Win32 USER and graphics device interface, or GDI, functions), such as dealing with windows, user interface controls, and drawing.

Figure 4.5 is a more detailed and complete diagram of the Windows 2000 system architecture and components that has shown earlier in Figure 4.4. The following sections elaborate on each major element of this diagram.

## 4.3.1 Environment Subsystems and Subsystem DLLs

As shown in Figure 4.4, Windows 2000 has three environment subsystems: OS/2, POSIX, and Win32. As we’ll explain shortly, of the three, the Win32 subsystem is special in that Windows 2000 can’t run without it. (It owns the keyboard, mouse, and display, and it is required to be present even on server systems with no interactive users logged in.) In fact, the other two subsystems are configured to start on demand, whereas the Win32 subsystem must always be running.

The role of an environment subsystem is to expose some subset of the base Windows 2000 executive system services to application programs. Each subsystem can provide access to different subsets of the native services in Windows 2000. That means that some things can be done from an application built on one subsystem that can’t be done by an application built on another subsystem. For example, a Win32 application can’t use the POSIX fork function.

Each executable image (.exe) is bound to one and only one subsystem. When an image is run, the process creation code examines the subsystem type code in the image header so that it can notify the proper subsystem of the new process. This type code is specified with the /SUBSYSTEM qualifier of the link command in Microsoft Visual C++ and can be viewed with the Extetype tool in the Windows 2000 resource kits.

![](img/e2283ffaea56e577ac05056b4bb738fc_104_0.png)

**Figure 4.5** Windows 2000 architecture.

Function calls can’t be mixed between subsystems. In other words, a POSIX application can call only services exported by the POSIX subsystem, and a Win32 application can call only services exported by the Win32 subsystem. As you’ll see later, this restriction is the reason that the POSIX subsystem, which implements a very limited set of functions (only POSIX 1003.1), isn’t a useful environment for porting Unix applications.

As mentioned earlier, user applications don’t call Windows 2000 system services directly. Instead, they go through one or more subsystem DLLs. These libraries export the documented interface that the programs linked to that subsystem can call. For example, the Win32 subsystem DLLs (such as Kernel32.dll, Advapi32.dll, User32.dll, and Gdi32.dll) implement the Win32 API functions. The POSIX subsystem DLL implements the POSIX 1003.1 API.

When an application calls a function in a subsystem DLL, one of three things can occur:

- The function is entirely implemented in user mode inside the subsystem DLL. In other words, no message is sent to the environment subsystem process, and no Windows 2000 executive system services are called. The function is performed in user mode, and the results are returned to the caller. Examples of such functions include GetCurrentProcess (which always returns −1, a value that is defined to refer to the current process in all process-related functions) and GetCurrentProcessId (the process ID doesn’t change for a running process, so this ID is retrieved from a cached location, thus avoiding the need to call into the kernel).

- The function requires one or more calls to the Windows 2000 executive. For example, the Win32 ReadFile and WriteFile functions involve calling the underlying internal (and undocumented) Windows 2000 I/O system services NtReadFile and NtWriteFile, respectively.

- The function requires some work to be done in the environment subsystem process. (The environment subsystem processes, running in user mode, are responsible for maintaining the state of the client applications running under their control.) In this case, a client/server request is made to the environment subsystem via a message sent to the subsystem to perform some operation. The subsystem DLL then waits for a reply before returning to the caller.

Some functions can be a combination of the second and third items above, such as the Win32 CreateProcess and CreateThread functions.

Although Windows 2000 was designed to support multiple, independent environment subsystems, from a practical perspective, having each subsystem implement all the code to handle windowing and display I/O would result in a large amount of duplication of system functions that, ultimately, would negatively affect both system size and performance. Because Win32 was the primary subsystem, the Windows 2000 designers decided to locate these basic functions there and have the other subsystems call on the Win32 subsystem to perform display I/O. Thus, the POSIX and OS/2 subsystems call services in the Win32 subsystem to perform display I/O. (In fact, if you examine the subsystem type for these images, you’ll see that they are Win32 executables.)

Let’s take a closer look at each of the environment subsystems.

### Win32 Subsystem

The Win32 subsystem consists of the following major components:

- The environment subsystem process (csrss.exe) contains support for
    - console (text) windows,
    - creating and deleting processes and threads,
    - portions of the support for 16-bit virtual DOS machine (VDM) processes, and
    - other miscellaneous functions, such as GetTempFile, DefineDosDevice, ExitWindowsEx, and several natural language support functions.

- The kernel-mode device driver (win32k.sys) contains two components:
    - The window manager, which controls window displays; manages screen output; collects input from keyboard, mouse, and other devices; and passes user messages to applications.
    - The Graphics Device Interface (GDI), which is a library of functions for graphics output devices. It includes functions for line, text, and figure drawing and for graphics manipulation.

- Subsystem DLLs (such as Kernel32.dll, Advapi32.dll, User32.dll, and Gdi32.dll) translate documented Win32 API functions into the appropriate undocumented kernel-mode system service calls to Ntoskrnl.exe and Win32k.sys.

- Graphics device drivers are hardware-dependent graphics display drivers, printer drivers, and video miniprint drivers.

Applications call the standard USER functions to create user interface controls, such as windows and buttons, on the display. The window manager communicates these requests to the GDI, which passes them to the graphics device drivers, where they are formatted for the display device. A display driver is paired with a video miniprint driver to complete video display support.

The GDI provides a set of standard two-dimensional functions that let applications communicate with graphics devices without knowing anything about the devices. GDI functions mediate between applications and graphics devices such as display drivers and printer drivers. The GDI interprets application requests for graphic output and sends the requests to graphics display drivers. It also provides a standard interface for applications to use varying graphics output devices. This interface enables application code to be independent of the hardware devices and
