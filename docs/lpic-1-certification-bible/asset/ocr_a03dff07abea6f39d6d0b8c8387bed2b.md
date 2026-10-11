10. D. This sets the maximum job size in 1KB blocks. For more information, see the “Installing Printers” section.

11. lprm 243. The `lprm` command removes print jobs. For more information, see the “Managing print jobs” section.

12. B. The `lpd` daemon should be restarted after any configuration changes. For more information, see the “Installing Printers” section.

13. A. `up`, `down`, and `disable` are valid commands, but `refresh` is not. For more information, see the “Managing printers” section.

14. A. The `release` command releases a job that’s on hold. For more information, see the “Managing printers” section.

15. B. The spool directory must be manually created, and the permissions and ownership must be set. For more information, see the “Creating the spool directory and log file” section.

16. C. The `stop all` directive must be used with `lpc`. For more information, see the “Managing printers” section.

17. B. This is the opposite of doing `lpc stop` and will enable a stopped printing device. For more information, see the “Managing printers” section.

18. D. This sends a file directly to the interface port. For more information, see the “Printer problems” section.

19. B. The `lpd` daemon is used to send remote print jobs. For more information, see the “Managing the printer daemon” section.

20. A. PrintTool provides an X GUI interface, and Magicfilter has no interface. For more information, see the “Using Print Filters” section.

# Scenarios

1. You should only consider writing your own print filters if you are very familiar with different file formats and the language your printer supports. You only need to write a new filter if the existing filters do not support your printer, or if you need to customize the way data is handled.

2. First, check to make sure the `lpd` daemon is still running by performing a `ps` check. Next, check to make sure spooling and printing is enabled with `lpc status`. Finally, check the queue status to make sure the jobs are not on hold. Finally, restart the `lpd` daemon for a fresh start. If printing still does not start, check the physical interface manually by sending a file directly to the device.