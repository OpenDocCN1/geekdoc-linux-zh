# lpq 731

The print client commands locate destination information in a specific order. See nswitch.conf(4), printer.conf(4) and printers(4) for details.

# Options

+   - P destination

Display information about printer or class of printers (see lpadmin(1M)). Specify destination using atomic, POSIX-style (server:destination) or Federated Naming Service (FNS) (.../service/printer/) names. See printers.conf(4) for information regarding the naming conventions for atomic and FNS names, and standards(5) for information regarding POSIX.

+   - 1

Display information in long format. Long format includes the name of the host from which a print request originated.

+   - [interval]

Display information at specific time intervals. Stop displaying when the print queue is empty. Clear the screen before displaying the print queue. Specify interval as the number of seconds between displays. If interval is not specified, execute only once.

# Operands

+   request-ID

The job number associated with a print request.

+   user

The name of the user whose jobs lpq reports information. Specify user as a valid username.

# Exit Status

+   0

Successful completion.

+   non-zero

An error occurred.

# Files

+   /var/spool/print/[cd] f*

Spooling directory and request files for jobs awaiting transfer.

# Attributes

See attributes(5) for descriptions of the following attributes:

| Attribute Type | Attribute Value |
| Availability | SUNwscplo |

# See Also

lpq(1), lpstat(1), lpc(1), lpr(1B), lprm(1B), lpadmin(1M), nswitch.conf(4), printers(4), printers.conf(4), attributes(5), standards(5)