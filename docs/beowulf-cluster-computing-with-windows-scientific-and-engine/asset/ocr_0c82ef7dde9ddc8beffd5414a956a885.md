![](bbox=[0.15, 0.17, 0.95, 0.45])

# **Figure 4.4**
Simplified Windows 2000 architecture.

The four basic types of user-mode processes are described as follows:

+   *   *Fixed* (or *hardwired*) *system support processes*, such as the logon process and the session manager, that are not Windows 2000 services (that is, is not started by the service control manager).

+   *   *Service processes* that host Win32 services, such as the Task Scheduler and Spooler services. Many Windows 2000 server applications, such as Microsoft SQL Server and Microsoft Exchange Server, also include components that run as services.

+   *   *User applications*, which can be one of five types: Win32, Windows 3.1, MS-DOS, POSIX, or OS/2 1.2.

+   *   *Environment subsystems*, which expose the native operating system services to user applications through a set of callable functions, thus providing an operating system *environment*, or personality. Windows 2000 ships with three environment subsystems: Win32, POSIX, and OS/2.

In Figure 4.4, notice the “Subsystem DLLs” box below the “Service processes” and “User applications” boxes. Under Windows 2000, user applications don’t call the native Windows 2000 operating system services directly; rather, they go through one or more *subsystem dynamic-link libraries*. The role of the subsystem DLLs is to translate a documented function into the appropriate internal (and undocumented) Windows 2000 system service calls. This translation might or might not involve sending a message to the environment subsystem process that is serving the user application.

The kernel-mode components of Windows 2000 include the following: