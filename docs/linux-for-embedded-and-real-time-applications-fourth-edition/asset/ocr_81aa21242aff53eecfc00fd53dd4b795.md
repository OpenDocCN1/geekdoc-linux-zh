Use these advanced breakpoint features to debug your thermostat program by entering different values for the A/D input into the devices program, and watch how the thermostat state machine responds.

When you feel the program is running correctly, rebuild it for the target board. You will need another make target. Call it, e.g., `ARMthermo`. Uncheck *Same as the target* name, and enter `all` for the Make target. Uncheck *Use builder settings*, and enter `make TARGET=1` for the Build command. Before making this target, delete `thermostat.o`. Otherwise, it will not be recompiled for the ARM, and the linker will complain about a bad object file.

To debug `thermostat_t` on the target, you will need to modify the debug launch configuration that you created for the measure program at the beginning of the chapter. Bring up the Debug Configurations dialog, and select the measure configuration. Change the name to "target," as we will use this configuration for all of our target debugging. Change the file name in C/C++ Application from `measure` to `thermostat_t`. Those are the only changes required. Click Apply.

On the target board, run `gdbserver:10000 thermostat_t`. Then back in Eclipse, click **Debug**. You are now debugging the thermostat program on the target board.

# ## Debugger Services Framework

For all its capability, the remote debugging process that we have seen so far is a bit tedious. You have to manually start `gdbserver` through the `minicom` shell, and that is where the program console is. Wouldn’t it be nice to have `gdbserver` start up automatically when you click **Debug**? And have the program I/O show up in an Eclipse console view. That is what the DSF does for us.

DSF is built on top of the Remote System Explorer (RSE), a collection of tools that allows you to work directly with resources such as files and folders on remote systems. RSE in turn uses SSH, the Secure Shell, to establish communication with remote systems.

# ### Configuring Remote System Explorer

Fire up Eclipse, and open the RSE perspective. You will find that the Project Explorer view on the left has been replaced by a view labeled Remote Systems, and the collection of views under the Editor has been replaced by something called Remote System Details. Right now, the only thing listed in Remote Systems is Local, your workstation. Expand that entry to reveal Local Files and Local Shells. Expand Local Files to browse the file system (Fig. 8.8).