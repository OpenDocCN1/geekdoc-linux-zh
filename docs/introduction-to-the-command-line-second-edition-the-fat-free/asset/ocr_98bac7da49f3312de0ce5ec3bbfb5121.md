# lpstat

**Purpose**: Display printer and print job status information.

**Usage syntax**: `lpstat [OPTIONS]`

```
```
$ lpstat
HP-4350-5     nick  1024  Tue 02 Jun 2009 12:56:50 PM CDT
HP-4350-6     nick  1024  Tue 02 Jun 2009 12:56:51 PM CDT
HP-4350-7     nick  1024  Tue 02 Jun 2009 12:56:52 PM CDT
HP-4350-8     nick  1024  Tue 02 Jun 2009 12:56:52 PM CDT
```
```

![](bbox=[0.25, 0.28, 0.8, 0.3])

The `lpstat` command displays information about printers and queued print jobs. In the above example, executing `lpstat` with no options displays the status of all queued print jobs.

The output of the `lpstat` command is defined in the following table.

| Field 1          | Field 2     | Field 3  | Field 4                    |
|:-----------------:|:-----------:|:--------:|:--------------------------:|
| PrinterName-JobID | Job owner   | Job size | Submission time and date   |

The `-a` option shows the status of all printers on the local system as demonstrated in the next example.

```
```
$ lpstat -a
HP-4350 accepting requests since Tue 02 Jun 2009 12:51:08 PM CD
HP-5100 accepting requests since Tue 02 Jun 2009 12:51:08 PM CD
```
```

![](bbox=[0.25, 0.66, 0.8, 0.68])

+   **Common usage examples:**
+   
+   |   |   |
+   |---|---|
+   | `lpstat` | Display the status of the print queue |
+   | `lpstat -a` | Display the current state of all printers |
+   | `lpstat -P` | Display the printing status of all printers |
+   | `lpstat -s` | Display a status summary |
+   | `lpstat -t` | Display all status information |