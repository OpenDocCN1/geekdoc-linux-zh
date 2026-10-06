
# TABLE 27-1

| Symbol | Description |
| --- | --- |
| r | The number of processes waiting for CPU time |
| b | The number of processes in uninterruptible sleep |
| swpd | The amount of virtual memory used (in MB) |
| free | The amount of physical memory not used (in MB) |
| buff | The amount of memory used as buffer space (in MB) |
| cache | The amount of memory used as cache space (in MB) |
| si | The amount of memory swapped in from disk (in MB) |
| so | The amount of memory swapped out to disk (in MB) |
| bi | Number of blocks received from a block device |
| bo | Number of blocks sent to a block device |
| in | The number of CPU interrupts per second |
| cs | The number of CPU context switches per second |
| us | Percent of CPU time spent running non-kernel code |
| sy | Percent of CPU time spent running kernel code |
| id | Percent of CPU time spent idle |
| wa | Percent of CPU time spent waiting for I/O |
| st | Percent of CPU time stolen from a virtual machine |

This is a lot of information. You probably don't need to record all of the values from the vmstat command; just will the free memory, and percent of CPU time spent idle, give you a good snapshot of the system status (and by now you can guess exactly how well to extract those values from the output).

You may also have noticed that the output from the vmstat command includes table heading information, which we obviously don't want in our data. To solve that problem, you can use the sed command to display only lines that have a numerical value in:

```
$ vmstat 1 2 | sed -n '/[0-9]/p'
1 0 172028 8564 5276 62244 9 28 160 157 5 289 5 0
0 0 178660 12845 4245 71890 8 10 80 22 127 124 3 186 10 0
```

## Part V Advanced Topics

That's better, but now we need to get only the second line of data. Another call to the editor can solve that problem:

```
$ vmstat | sed -n '/[0-9]/p' | sed -n '2p'
0 178660 12845 4245 71890 8 10 22 127 124 3 1 86 10 0
```

Now you can easily extract the data value you want using the awk command.

Finally, you'll want to tag each data record with a date and timestamp to indicate when the snapshots were taken. The default output from the date command might be a little cumbersome. You can simplify the date command output by specifying format:

```
$ date +"%m/%d/%Y %k:%M:%S"
02/05/2008 19:19:26
```

That should look much better in our output. Speaking of the output, you should also consider how you want to record the data values.

For data that you sample on a regular basis, it's best to output the data directly to a log file. You can create the log file in your HOME directory, appending data each time you run the shell script. When you want to see the results, you can just view the log file.

You should spend some time considering the format of the log file. You'll want to ensure that the data in the log file can be read easily (after all the whole purpose of this script).

There are many methods you can use to format the data in the log file. A popular format is comma-separated values (CSV). This format places each record of data on a separate line, and separates the fields in the record with commas. This is a popular format for people who love spreadsheets, as it's easily imported into a spreadsheet.

However, staring at a CSV file of data is not the most exciting thing in the world. If you want to provide a more aesthetically appealing report, you can create an HTML document.

HTML is the standard method for formatting Web pages. It uses simple tags to delineate data types within the Web page. However, HTML is not just for Web pages. You'll often find HTML used in e-messages as well. Depending on the MUA client (see Chapter 26), you may or not be able to view an embedded HTML e-mail. A better solution is to create the HTML report, and attach it to the e-message.

The script will save data in a CSV-formatted file, so you can always access the raw data to import data into a spreadsheet. When the system administrator runs the report script, that will reformat the data into an HTML report. How cool is that?

## Creating the capture script

Since you need to sample system data at a regular interval, you'll need two scripts. One script will capture the data and save it to the log file. This script should run on a regular basis

# Shell Scripts for Administrators from the cron table. The frequency depends on how busy your Linux system. For most systems, running the script once an hour should be fine.

The second script will output the report data and e-mail it to the appropriate individual(s). Most likely you won't want to e-mail a new report every time you get a new data sampling. You'll probably want to run the script as a cron job at a lower frequency, such as once a day, first thing in the day.

The first script, used to capture the data, is called capstats. Here's what it looks like:

```
$ cat capstats
!/bin/bash
# script to capture system statistics
```

```
OUTFILE=/home/rich/capstats.csv
DATE=date +%m/%d/%Y
TIME=date +%k:%M:%S

TIMEOUT=`uptime`
VMOUT=`vmstat 1 2`

USERS=$(echo $VMOUT | awk '{print $4}' | sed 's/,///')
FREE=$(echo $VMOUT | sed -n '/[0-9]/p' | sed -n '2p' | awk '{print $4}')
IDLE=$(echo $VMOUT | sed -n '/[0-9]/p' | sed -n '2p' | awk '{print $15}')
```

```
echo "\$DATE,$TIME,$USERS,$LOAD,$FREE,$IDLE" >> \$OUTFILE
$
```

This script mines the statistics from the uptime and vmstat commands and saves them in variables. The script then writes the values to the file defined by the $OUTFILE variable. For this example, I just saved the file in my $HOME directory. You might modify this location to suit your environment best.

After creating the capstats script, you should probably test it from the command line before running it regularly from your cron table:

```
$ ./capstats
$ cat capstats.csv
02/06/2008:10:39:57,4.0,26,57076,887
$
```

The script created the new file, and placed the static values in the proper places. Just to make sure that subsequent runs of the script do not overwrite the file, test it again:

```
$ ./capstats
$ cat capstats.csv
02/06/2008,10:39:57,4.0,26,57076,887
02/06/2008,10:39:57,4.0,26,57076,887
$
```

As hoped, the second time the script ran it appended the new statistics to the end of the file. Now you're ready to place it once hour, create this cron entry:

```
0 * * * * /home/rich/capstats
```

## Generating the report script

Now that you have a file of data, you can start working on the script to generate a fancy report. The best tool for this is gawk. First, test this from the command line, using the new capstats.csv file:

```
$ cat capstats.csv | gawk -F, '{printf "%s %s %s\n", $1, $2, $4}'
02/06/2008 10:39:57 26
02/06/2008 10:41:52 14
02/06/2008 10:50:01 06
02/06/2008 11:00:01 18
02/06/2008 11:10:01 03
02/06/2008 11:20:01 07
$
```

You need to use the -F option for the gawk command to define the comma as the separator character in your data. After that, you can retrieve each individual data field and display it as you need.

For the report, we will be using HTML format. This allows us to create a nicely formatted report with a minimum amount of work. The browser that displays the report will do all the hard work of formatting and displaying the report. All you need to do is insert the appropriate HTML tags to format the data.

The easiest way to display spreadsheet data in HTML is using the <table> tag. The table allows you to create a table with rows and cells (called divisions in HTML-speak). You define the start of a row using the `<tr>` tag, and the end of the row with the `</tr>` tag. Similarly, you define cells using the `<td>` and `</td>` tag pair.

The HTML for a full table looks like this:

```html
<html>
<body>
<h2>Report title</h2>
<table border="1">
```
