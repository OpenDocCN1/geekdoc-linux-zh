# Table 8.2   Print-related commands in Linux.

| Command | Purpose |
| :--- | :--- |
| **lpc** | Printer control program |
| **lpd** | Print daemon |
| **lpq** | Print spool control program |
| **lpr** | The print spooler |
| **lprm** | Print job removal |
| **pac** | Generates print accounting reports |

them out for you here in Table 8.2. Each has a specific function in the greater
scheme of print job and printer management.

# The Printer Control Program

You use the **lpc** command in the format:

```
lpc command value
```

The available commands are listed in Table 8.3.

# Table 8.3   Available commands for *lpc*.

| Command | Purpose | Values |
| :--- | :--- | :--- |
| **?** | Prints help information about a command. | **lpc** command |
| **abort** | Kills the active print daemon that manages this printer's spool, then disables printing to this printer. | Either **all** for every printer, or the printer name for the specific printer |
| **clean** | Removes any unprintable files from the printer's queue. Good for cleaning out temporary information. | Either **all** for every printer, or the printer name for the specific printer |
| **disable** | Turns the printer's queue off so it will not pull any more jobs from the spool. | Either **all** for every printer, or the printer name for the specific printer |
| **down** | Turns the printer's queue off and does not allow new jobs to be spooled. | Either **all** for every printer, or the printer name for the specific printer; plus a brief message explaining why the printer is down |
| **enable** | Turns the printer's queue on so new jobs can be spooled. | Either **all** for every printer, or the printer name for the specific printer |
| **help** | Prints help information about a command. | **lpc** command |

*(continued)*