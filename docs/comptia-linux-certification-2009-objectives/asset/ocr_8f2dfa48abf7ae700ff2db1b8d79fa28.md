# TOPIC B

# Print Files

You configured a compatible printer to work with a Linux system. With the printer installed, you are ready to print files. In this topic, you will print files in the Linux system.

Printing a file is a routine task. Learning to print in Linux will save you time when documenting system information and changes. While you can print from the GUI, learning to print from the command line will give you greater freedom when printing from another location.

# Printer Commands

![](bbox=[0.05, 0.3, 0.17, 0.37])

Linux comprises various commands that facilitate the printing process. Some of the commands are described in the following table.

| Command | Description |
| :--- | :--- |
| lp | Submits files for printing or alters a pending print job. The syntax of this command is `lp [command options] (file name)`. |
| lpr | Submits files for printing. Files entered on the command line are sent to the specified printer or to the print queue if the printer is busy. If no files are entered on the command line, the `lpr` command reads the print file from the standard input. The syntax of this command is `lpr [command options] (file name)`. |
| lpq | Displays the current print queue status. The syntax of this command is `lpq [command options] (Print queue name)`. |
| lpshm | Cancels print jobs in the queue. The syntax of this command is `lprm (print job id)`. |
| lpc | Allows you to start or stop a printer, enable or disable queues, manage jobs in the queue, and obtain a status report on the printers and queues. The syntax of this command is `lpc [parameter]`. |
| lpstat | Displays CUPS status information. The syntax of this command is `lpstat [command options]`. |
| cancel | Deletes a print job from the print queue. The syntax of this command is `cancel [command options]`. |