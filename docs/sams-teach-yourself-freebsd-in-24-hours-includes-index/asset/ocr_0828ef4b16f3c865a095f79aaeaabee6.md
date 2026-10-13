# Configuring the Printer

At this point, we are going to assume that you have a relatively recent printer that is plugged in to your computer's parallel port. We aren't going to cover serial printers, which are relatively obsolete.

The first thing you will want to do is set the parallel port mode.

# Configuring the Parallel Port

The lptcontrol program can be used to configure the mode of the parallel port. You will need to be logged in as the root user to do this. In its basic form, lptcontrol is run with an option that you wish to set on the port. The following options are supported:

| Option | Description |
|---|---|
| -i | Sets interrupt driven mode |
| -p | Sets polled mode |
| -e | Sets extended mode |
| -s | Sets standard mode (that is, turns off extended mode) |

The option you will probably be most interested here is -e. If your printer supports an extended mode such as ECP or EPP, and you have this configured in your BIOS, you will want to turn this option on with the lptcontrol command. The following command shows how this is done:

```
lptcontrol -e
```

Basically, extended modes allow additional features to simple printing, such as allowing the printer to communicate back to the computer and inform the computer of error conditions such as paper jams or if it runs out of ink. In standard printer mode (that is, no extended mode), data can only be sent one way from the computer to the printer. The printer has no way to communicate back with the computer.

By default, lptcontrol assumes the default printer port, which is /dev/lpt0 in FreeBSD. This will be the first parallel port on the system, which corresponds to LPT1 in Windows. If you have more than one parallel port, and this printer is not on the first one, you can use the -d option to specify a different port. For example, if you want to enable extended mode on the second parallel port, you could use the following command:

```
lptcontrol -e -d /dev/lpt1
```

Note that this setting will be lost when you reboot the system. If you want to have it maintained after each reboot, you need to add it to a system startup script. The best way