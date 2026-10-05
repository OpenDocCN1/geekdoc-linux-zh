of, if: printing filters

over control of the printer. It also gives you a single place to look when printing is
not working.

Remote machines (machines that are not directly connected to the printer) have
simple printcap entry that tells where to send the job, as in the example on page
1060. The rm variable specifies the machine to which jobs should be sent, and the
pr variable gives the name of the printer on that machine.

The fact that printcap entries are different for local and remote printers necessary-
tates a bit of subteruge on the part of the system administrator if one printcap is
to be shared among several machines. The fix is to make the local and remote
names for a printer distinct; for example, howlr-local and howlr-lw. This
configuration makes howlr-lw a "remote" printer even on the machine where it
alives, but that's perfectly OK. You must refer to howlr-lw if you
mant to use the lpc command, however.

of, if: printing filters

Filters serve several purposes. The default filter (usually /usr/lib/lpf)
fixes up various nonprinting sequences and writes out an account record if
appropriate. Unfortunately, filters are not standardized. Any of several filter pack-\ages could do the same job, but each vendor tends to use unique filters.

If you have a laser or inkjet printer, or an ancient typesetter or plotter, the
necessary filters will usually have been provided with the printer software. If you
to configure a printer for which you have no software, read through the de-	ails in the rest of this section. Otherwise, skip ahead; ignorance is bliss.

Filters are usually just shell scripts that call a series of translation programs. The
filter program must accept the print job on standard input, translate the job to a
format appropriate for the device, and send the result to standard output.

If the user does not specify a filter when executing lpr, either the if (input filter) or
of (output filter) is used. The names are deceptive—both actually send data to
a printer.

If the printcap enters an input filter but does not specify an output filter, the
device is opened for each job. The filter is expected to send one job to the
printer and then.

Conversely, if an output filter is specified without an input filter, lpd opens the
device once and calls the filter program once, sending all the jobs in the queue in
big clump. This convention is OK for devices that take a long time to connect;
hhowever, such devices are extremely rare.

If both an input filter and an output filter are specified, the banner page is sent to
t output filter, and the output filter is called even if banners are turned off. The
input filter is to process the rest of the job. This combination of options is
real too confusing for mere mortals. Avoid it.

![](bbox=[0.953, 0.532, 0.997, 0.626])