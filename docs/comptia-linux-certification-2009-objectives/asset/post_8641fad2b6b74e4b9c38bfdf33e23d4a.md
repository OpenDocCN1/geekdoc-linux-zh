
## TOPIC B

### Print Files

You configured a compatible printer to work with a Linux system. With the printer installed, you are ready to print files. In this topic, you will print files in the Linux system.

Printing a file is a routine task. Learning to print in Linux will save you time when documenting system information and changes. While you can print from the GUI, learning to print from the command line will give you greater freedom when printing from another location.

### Printer Commands

![](img/477ccb2f05b6ba1b2d563ea74f18c197_251_0.png)

Linux comprises various commands that facilitate the printing process. Some of the commands are described in the following table.

| Command | Description |
| :--- | :--- |
| lp | Submits files for printing or alters a pending print job. The syntax of this command is `lp [command options] (file name)`. |
| lpr | Submits files for printing. Files entered on the command line are sent to the specified printer or to the print queue if the printer is busy. If no files are entered on the command line, the `lpr` command reads the print file from the standard input. The syntax of this command is `lpr [command options] (file name)`. |
| lpq | Displays the current print queue status. The syntax of this command is `lpq [command options] (Print queue name)`. |
| lprm | Cancels print jobs in the queue. The syntax of this command is `lprm (print job id)`. |
| lpc | Allows you to start or stop a printer, enable or disable queues, manage jobs in the queue, and obtain a status report on the printers and queues. The syntax of this command is `lpc [parameter]`. |
| lpstat | Displays CUPS status information. The syntax of this command is `lpstat [command options]`. |
| cancel | Deletes a print job from the print queue. The syntax of this command is `cancel [command options]`. |

### The lpr Command

The `lpr` command comprises various options that allow you to specify the nature of print output.

| Option | Used To |
|---|---|
| -E | Force encryption when connecting to the server. |
| -P destination | Print files with the destination printer specified. |
| -# copies | Set the number of copies to print from 1 to 100. |
| -C name | Set the job name. |
| -l | Specify that the print file is already formatted and sent without being filtered to the destination. |
| -o option | Set a job option. |
| -f | Specify that the print file needs to be formatted with a shaded header that includes the date, time, job name, and page number of the file. |
| -r | Specify that the print files should be deleted after being printed. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_252_0.png)

### The lpc Command

The `lpc` command comprises various options that allow you to manage print jobs.

The following table lists the frequently used `lpc` command options to control a print job.

| Option | Used To |
|---|---|
| lpc defaultq | View the default queue for the printer. |
| lpc hold [Print queue name] [Job ID] | Hold the specified printer job in the queue. |
| lpc holdall [Print queue name] | Hold all new jobs given to the specified queue. |
| lpc release [Print queue name] [Job ID] | Release the print job that has been put on hold. |
| lpc noholdall [Print queue name] | Turn off the holdall option and allow all new print jobs to be executed (the jobs that were put on hold after running the holdall option should be activated using the release option). |
| lpc lpd | Determine if the lpd daemon is running. |
| lpc move [Print queue name] [Job ID] [Destination queue name] | Move the specified job to a different print queue. |
| lpc topq [Print queue name] [Job ID] | Place the specified job at the top of the print queue. |
| lpc lpq | View print jobs in the queue. |
| lpc lprm [Print queue name] [Job ID] | Remove print jobs from the queue. |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_252_1.png)

### The pr Command

The `pr` command formats files before they are printed. By default, the `pr` command sends its output to the terminal screen, but is also used in combination with commands that send output to a printer. The `pr` command formats the files’ header containing the page number, file name, date, and time.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_253_0.png)

#### Syntax

The syntax of the `pr` command is `pr [command options] {file name}`.

![](img/477ccb2f05b6ba1b2d563ea74f18c197_253_1.png)

### The pr Command Options

There are many formatting options available for use with the `pr` command.

| Option | Description |
| :----- | :----- |
| -column | Produces a multi-column output with the data arranged in columns. |
| -d | Produces a double-spaced output. |
| -m | Merges files. |
| -F | Wraps the lines of the input files to fit the column width. |
| -l[#] | Changes the page length of the output, where # is the number of lines per page. |
| -h[new header text] | Allows you to change what is included in the header at the top of each page, where [new header text] replaces the file name in the default header contents. |

### Using pr with Piping

When you format your output with the `pr` command, you can send the formatted output to a file to be printed using the redirection operators (>) and pipe. For example, `pr -l 45 sales > sales.out` creates the `sales.out` file, which is formatted and ready for printing. In addition, you can send the formatted file directly to the printer using the `lpr` command. For example, the `pr -l 45 sales | lpr` command sends the formatted sales file directly to the default printer.

### How to Print Files

#### Procedure Reference: Print a File Without Text Formatting

To print a file without text formatting:

1. Change to the directory that contains the file you want to print.
2. Print the file using `cat [file name] | lpr`.

#### Procedure Reference: Print a File With Text Formatting

To print a file with text formatting:

1. Change to the directory that contains the file you want to print.
2. Enter `pr [options] ({file name}) | more` to view the file with text formatting.
3. Enter `pr [options] ({file name}) | lpr` to print the file with text formatting.

### **ACTIVITY 6-3**
**Formatting Text for Printing**

**Before You Begin:**

1. You have logged in as root in the GUI.
2. Display the terminal window.

**Scenario:**
Due to recent changes in the boot process and a hard disk upgrade, your manager asked you to print copies of system files for record keeping. Any further changes to these files should be documented and a new version should be printed. You decide to use text formatting features to fix any alignment issue before printing the files.

| What You Do | How You Do It |
| :--- | :--- |
| 1. Display the contents of the /etc/fstab and /etc/inittab files using the more command. | a. Enter `more /etc/fstab` to view the contents of the /etc/fstab file. |
| | b. Observe the contents of the /etc/fstab file displayed on the screen. |
| | c. Enter `more /etc/inittab` to view the contents of the first page of the /etc/inittab file. |
| | d. Press the **Spacebar** to view the next page of the /etc/inittab file. |
| | e. Observe the contents of the /etc/inittab file displayed on the screen. |
| | f. Press the **Spacebar** to view the remaining part of the file. |
| 2. Display the /etc/inittab file using the pr command. | a. Enter `pr /etc/inittab \| more` |
| | b. Observe that the date, title, and page number are displayed. |
| | c. Press the **Spacebar** to view the next page of the /etc/inittab file. |
| | d. Press the **Spacebar** to view the remaining part of the file. Observe the contents of the /etc/inittab file as displayed on the screen. |
| 3. Preview the /etc/fstab file with double line spacing and the heading "The fstab entries." | a. Enter `pr -d -h "The fstab entries" /etc/fstab | more` to preview the formatting applied to the file. |
| | b. Observe that "The fstab entries" is displayed as the heading and the file has double spacing between the lines. |
| | c. Press **Q** to close the preview and return to the command prompt. |
| 4. Preview the /etc/inittab file contents, 30 lines at a time using the `pr` command. | a. Enter `pr -l 30 /etc/inittab | more` |
| | b. Press the **Spacebar** to view the next page of the /etc/inittab file. |
| | c. Press the **Spacebar** to view the remaining parts of the file. Observe the contents of the /etc/inittab file as displayed on the screen. |
| | d. Enter `clear` to clear the terminal. |
| 5. Print the /etc/inittab file with text formatting and the /etc/fstab file with and without text formatting. | a. Enter `pr -l 30 /etc/inittab | lpr` to print the /etc/inittab file, 30 lines per page. |
| | b. Enter `pr -d -h "The fstab entries" /etc/fstab | lpr` to print the /etc/fstab file with "The fstab entries" as the heading and with double line spacing. |
| | c. Enter `cat /etc/fstab > lpr` to print the file without formatting. |
