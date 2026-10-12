|Action|How the Command Is Run|
| boot|The command is executed during the system boot phase, after all sysinit entries have been processed; the runlevels field is ignored.|
| bootwait|The same as boot, but it waits for the command to finish before continuing with other inittab entries; the runlevels field is also ignored.|
| initdefault|The run level to enter after completing the boot and sysinit actions.|
| off|Nothing happens (perhaps useful for testing and debugging).|
| ctrlaltdel|Traps the Ctrl+Alt+Del key sequence, and is typically used to gracefully shut down the system.|
| kbdrequest|Used to trap special key sequences, as interpreted by the keyboard handler.|

# Breakdown of the inittab file

Because the inittab file is a configuration file, not a sequential shell script, the order of lines is not significant. Lines beginning with a hash (#) character are comments and are not processed.

The first non-commented line in the preceding sample inittab file sets the default run level to 3. A default of 3 means that, following the completion of all commands associated with the sysinit, boot, and bootwait actions, run level 3 will be entered (booting to a text-based login). The other common initdefault level is run level 5 (booting to a GUI login screen). Table 12-4 describes each of the run levels and helps you choose the run level that is best suited as the default in your environment.

# Table 12-4: Possible Run Levels

|Run Level|What Happens in This Run Level|
| 0|All processes are terminated and the machine comes to an orderly halt. As the inittab comments point out, this is not a good choice for initdefault, because as soon as the kernel, modules, and drivers are loaded, the machine will halt.|
| 1, s, S|This is single-user mode, frequently used for system maintenance and where it may be preferable to have few processes running and no services activated. In single-user mode, the network is nonexistent, the X server is not running, and it is possible that some file systems are not mounted.|