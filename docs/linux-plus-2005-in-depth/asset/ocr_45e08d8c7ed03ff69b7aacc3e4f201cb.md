# PRINTER ADMINISTRATION

The lp command uses the -d option to specify the destination printer name. If this option is omitted, the lp command assumes the default printer on the system. Because printer1 is the only printer on the system and, hence, is the default printer, the command lp /etc/initab is equivalent to the one used in the preceding output.

![](bbox=[0.17, 0.23, 0.21, 0.27])

# **NOTE**

> You can set the default printer for all users on your system by using the lpoptions -d printername command, where printername is the name of the default printer. This information is stored in the /etc/cups/lpoptions file.
> 
> Each user on a Linux system can specify his own default printer by adding the line default printername to the .lpoptions file in his home directory, where printername is the name of the default printer. Alternatively, you can use the PRINTER or LPDEST variables to set the default printer. For example, to specify printer2 as the default printer, you can add either the line export PRINTER=printer2 or the line export LPDEST=printer2 to an environment file in your home directory such as .bash_profile.

Table 11-1 lists some common options to the lp command.

**Table 11-1 Common options to the lp command**

| Option | Description |
|---|---|
| -d *printername* | Specifies the name of printer to send the print job. |
| -i *print job ID* | Specifies a certain print job ID to modify. |
| -n *number* | Prints a certain *number* of copies. |
| -m | Mails you confirmation of print job completion. |
| -o *option* | Specifies certain printing options. Common printing options include the following:<br>*cpi = number*—Sets the characters per inch to *number*<br>*landscape*—Prints in landscape orientation<br>*number-up = number*—Prints *number* pages on a single page, where *number* is 1, 2, or 4<br>*sides = string*—Sets double-sided printing, where *string* is either ‘two-sided-short-edge’ or ‘two-sided-long-edge’ |
| -q *priority* | Specifies a print job priority from 1 (low priority) to 100 (high priority). By default, all print jobs have a priority of 50. |