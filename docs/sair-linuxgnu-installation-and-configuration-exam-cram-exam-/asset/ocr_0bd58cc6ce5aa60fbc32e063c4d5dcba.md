# lpq

The line printer query (lpq) command gives you the current print queue. Examples of this command are shown in Table 9.2. This command also includes a list of job numbers, which you might need for the lprm command.

# lprm

If a print job isn't already in your printer's memory, the line printer remove (lprm) command can delete print jobs currently in your queue. With lprm, you can remove a print job in one of three ways: by print job number, by user, or by printer. Examples of this command are shown in Table 9.3.

Users can use lprm to remove their own print jobs. The root or superuser can use this command to remove anyone's print job.

# lpc

The line printer control (lpc) command allows you to control a number of characteristics of each printer. As shown in Table 9.4, this command lets you check printer status, kill active print jobs, or even redirect jobs to a different printer.

# Printer Languages

When you want to print a file, Linux translates the file into a format that your printer can use. Printers have their own fonts embedded in their memory. If you're just printing text, Linux can send ASCII codes to your printer, which are translated into your printer's fonts. This is commonly known as text-mode printing.

Table 9.2 lpq commands.

| Command | Result |
|---|---|
| lpq | Returns the current print queue for the default printer, as defined in your /etc/printcap file. |
| lpq -P print1 | Returns the print queue for the print1 printer. Substitute a printer name based on the name shown in your /etc/printcap file. |

Table 9.3 lprm commands.

| Command | Result |
|---|---|
| lprm 188 | Removes print job 188, as defined in the output to the lpq command. |
| lprm -P hp2 mj | Removes print jobs of user mj from the printer labeled hp2 in your /etc/printcap file. |