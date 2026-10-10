# vparesset - Sends a TOC or hard reset to a virtual partition

vparesset (lM)                                                                                                                 vparesset (lM)

NAME
dparesset - reset a virtual partition

SYNOPSIS
dparesset -p vp_name [-h|-t] [-q] [-f]

DESCRIPTION
The vparesset command simulates, at the virtual partition level, the RS and TOC operations at a Control-B prompt on the system console.

Only a superuser can execute the vparesset command.

vparesset causes the virtual partition monitor to simulate a hard (RS)
reset or soft (TOC) reset of the specified virtual partition. Either
operation gathers new Processor Information Module (PIM) data, which
is displayed unless the -q (quiet) option is also specified.

Unintentional use of the vparesset command has serious consequences;
therefore the user is prompted to confirm the operation unless the -f
(force) option is specified.

Options
vpareset recognizes the following command line options and arguments:

+   - -p vp_name          Specifies the unique name of the virtual partition
+                         to be reset. The virtual partition must be in a
+                         state other than Down or Crashing. Required.
+       - t               Simulates a TOC reset. Displays current PIM data
+                         before resetting unless the -q option is also
+                         specified.
+   
+                         The TOC reset is also the default operation of the
+                         command, applied if neither the -h nor -t option
+                         is specified.
+   
+                         The -t and -h options cannot both be specified in
+                         the same command.
+       - h               Simulates a hard (RS) reset instead of a TOC.
+                         Displays current PIM data before resetting unless
+                         the -q option is also specified.
+       - q               Bypasses the display of current PIM data when
+                         resetting the virtual partition.
+       - f               The force option. Omits the confirmation dialog

![](bbox=[0.06, 0.08, 0.15, 0.18])