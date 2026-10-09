Manager (WebSM) to switch between subsystems. In either case, the **switch.pr** command is executed.

Eight steps are involved in switching between subsystems. To switch from the AIX print subsystem to the System V subsystem, use the **switch.pr** command.

+   Checks to see if any print jobs are currently active. If any printing is active, the **switch.pr** command exits with the following error message:

All print jobs must be terminated.

+   Stops the following AIX print daemons: lpd, qdaemon, and writersrv.

+   Changes the /etc/inittab file to start only the System V print subsystem daemons on all subsequent reboots.

+   Clears the SMIT menus that control the AIX print subsystem. However, some are not removed, but if you attempt to use them, you will receive an error message.

+   Modifies the WebSM to use only the System V plug-ins.

+   Changes the lock files from AIX to System V.

+   Changes all links from AIX to System V.

+   Starts the System V print subsystem daemon, lpsched.

To switch from the System V print subsystem to the AIX subsystem, use the **switch.pr** command

+   Checks to see if any print jobs are currently active. If any printing is active, the **switch.pr** command exits with the following error message:

All print jobs must be terminated.

+   Stops the System V print daemon, lpsched, using the lpsut command.

+   Changes the /etc/inittab file to start only the AIX print subsystem daemons on all subsequent reboots.

+   Enables the SMIT menus that control the AIX print subsystem.

+   Modifies the WebSM to use only the AIX plug-ins.

+   Changes the lock files from System V to AIX.

+   Changes all links from System V to AIX.

+   Starts the AIX print subsystem daemons, lpd, qdaemon, and writersrv.

After the printer subsystem has been switched, any disabled printers or print queues will remain disabled until you enable all of the print queues. Also, if a user tries to submit a print job using the qprt or enq command under System V control, an error message will be displayed:

Cannot awaken qdaemon (requested accepted anyway)

When, and if, the AIX printer subsystem is reestablished, the job will print.