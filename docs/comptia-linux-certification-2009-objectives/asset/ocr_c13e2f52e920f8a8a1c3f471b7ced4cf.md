The **pgrep** command is used to look up or signal processes based on their names or other attributes. It looks through the currently running processes and lists PIDs that match the criteria you specify. For instance, the **pgrep -u root sshd** command lists only processes called sshd and that are owned by the **root** user. The command **pgrep -u root,daemon** lists all processes owned by root or daemon.

The **pkill** command can be used in conjunction with the **pgrep** command to stop processes. Starting and stopping processes is just one more way to troubleshoot problems. When you see a certain symptom, such as a process taking too long, you should first check on the process using the **ps** or **pgrep** command; then if necessary, end the process using the **kill** or **pkill** command. Then, you should examine the process (the script or other command sequences associated with that process) and check for any problems. After fixing the problems, you should try running the command or script again. Check on it periodically to see if it is working properly.

![](bbox=[0.06, 0.335, 0.12, 0.39])

# # Hardware Problems

Hardware devices may experience failures anytime while the system is being used.

| Symptom | Cause And Solution |
|---|---|
| The user is unable to hear from the speakers. | **Cause**: The speaker or the sound card is not functioning properly.\n\n**Solution**: Check the speaker and its corresponding driver. If you still have a problem, then you need to check the sound card. |
| The modem is unable to dial in or out. | **Cause**: There is a mismatch between the modem configuration and the modem settings, or there could be a modem failure.\n\n**Solution**: Check the modem and serial port settings. If the problem continues, check the corresponding drivers. |
| When the system boots, the monitor switches to the power save mode or the power light flickers. | **Cause**: The CPU is unable to establish a link with the monitor.\n\n**Solution**: Check if the monitor cable is connected to the system and then check the functionality of the VGA card. |
| The dumb terminal device is unable to boot. It just stops with the display screen. | **Cause**: The dumb terminal is unable to connect with the server.\n\n**Solution**: Check the serial ports and cables. |
| A system connected to the UPS shuts down abruptly. | **Cause**: The UPS is malfunctioning, or there is a mismatch between the UPS settings and the configuration file.\n\n**Solution**: Check the serial ports, the cable, and the configuration file. |
| The user is unable to switch to the GUI mode. | **Cause**: The mouse does not function properly due to the configuration settings or there could be a problem in the device.\n\n**Solution**: Unplug and reconnect the mouse, then restart the system. |