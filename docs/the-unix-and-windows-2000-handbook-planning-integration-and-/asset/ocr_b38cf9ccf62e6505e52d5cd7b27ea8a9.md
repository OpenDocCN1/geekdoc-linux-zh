+   2. The system paging files are set up based on the entries defined in HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management\Paging-Files.

+   3. The HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\DosDevices Registry value is examined and the specified filesystem links are created.

+   4. The HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Subsystems\Required value is examined and the required subsystems are loaded. By default, only the Win32 subsystem is required.

# STARTING THE WIN32 SUBSYSTEM

If all of the previous phases have completed, the Win32 subsystem is loaded and performs the following tasks:

+   1. The WINLOGON.EXE program starts, which in turn starts the Local Security Authority (LSASS.EXE). When this is completed, the familiar Ctrl+Alt+Del message is displayed, indicating that the system is ready for a user to begin the logon process. This message box is shown in Figure 3.7.

+   2. The Service Controller (SCREG.EXE) is executed and makes one last pass through the Registry to locate and start any devices and services set to start automatically. This includes starting the workstation and server services, which are required for network access. Services and drivers are loaded on the dependencies specified in the Registry. It is a good idea not to attempt a logon (especially if you are in a networked environment) until all of the services and drivers have been loaded (i.e., the disk has stopped chattering).

Figure 3.7
Windows 2000 logon message.

![](bbox=[0.27, 0.82, 0.78, 0.98])