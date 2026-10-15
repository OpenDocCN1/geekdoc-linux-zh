# Managing Printer Queues

Your Linux distribution provides tools to help you control printing. These tools come in the form of several commands you can enter at an xterm or text-mode login. Some of these allow you to do things as an ordinary user; others may require you to be root. Most of these commands take at least the -P parameter to specify the printer queue on which you want to operate. When you use -P, type the name of the printer queue without an intervening space; for instance, lpq -Pcanon to query the printer queue called canon. Without the -P parameter, these commands work on the default printer queue, which is generally called lp.

You need to have a login account on the Linux computer to use these options; you can't control print jobs remotely in this way, except by using telnet, ssh, or a similar remote login tool. Samba provides some means for controlling printers remotely using standard Windows printer-control methods, so if you configure Samba correctly, you can perform similar actions from the client computer.

# Viewing Print Jobs by Using lpq

You use the lpq command to determine what print jobs are present in a print queue and whether that queue is printing. Here's some sample output showing a number of files in a printer queue:

```
Rank Owner Job Files Total Size
active rodsmith 152 /tmp/.pp_0000012278_58 10832657 bytes
1st rodsmith 153 /tmp/.pp_0000012335_59 23967 bytes
2nd rodsmith 154 /tmp/.pp_0000012365_60 22107 bytes
```

This output shows three print jobs in the queue, all started by the user rodsmith. Different programs place files in the print queue in different ways, so the names listed under the Files column might take different forms for different programs' print jobs. The first job is the one that's labeled active in the Rank column and has a job ID of 152. When the lpq command was issued, that job was being sent to the printer, hence its active status. The second and third jobs have ranks of 1st and 2nd and IDs of 153 and 154, respectively, and are waiting in the queue. The size of the active job is about 1MB, and the next two are each less than 24KB.

When you're doing additional print job management, you need to know the job ID listed under the Job column. The job size may or may not be helpful in determining which job is which. If you print two jobs from the same program to the same printer, the document with more pages is likely to be larger, but that might not be the case if the documents use different features (for example, if one is graphics and the other is text).