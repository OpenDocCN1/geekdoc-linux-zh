
The host submitting the print job has a couple of special settings in the `/etc/printcap` entry for the remote server's printer. `rm` is for remote machine and `rp` is for remote printer. A typical remote printer entry is shown here:

```
remotepr: \
:ml=0 \
:mx=0 \
:sd=/var/spool/lpd/remotepr \
:af=/var/spool/lpd/remotepr/remotepr.acct \
:sh \
:rm=192.168.1.2 \
:rp=brother \
:lpd_bounce=true \
:if=/usr/share/printconf/util/mf_wrapper
```

Notice that no local `lp=dev/lp` line appears in this configuration. The `rm=192.168.1.2` and `rp=brother` lines take its place and send the print jobs submitted to this printer to the remote system's `lpd` daemon for submission into the `brother` printer's spool directory.

> **Note:** The `rm` and `rp` entries are likely to be on the exam, so make sure that when you're shown an `/etc/printcap` print-out, that you look carefully to see where the printer points and what other parameters are present.

## Printing Command Overview

Several commands are used in the `lpd` style of printing. The following table lists them, and examples are presented in the later sections.

| Command | Description |
| :------- | :---------- |
| `lpd` | The `lpd` daemon itself. All printers defined on the system get an instance of `lpd` to themselves. |
| `lpr` | Used to submit print jobs. `lpr` uses the default printer if none is specified. |
| `lpq` | Used to query the default printer, specific printers, or all printers. |
| `lprm` | Used to remove print jobs from the default, specific, or all queues. |
| `lpc` | Used to configure the `lpd` daemon and printers either from the command line or interactively. |

> **Note:** The original version of `lpd` and its associated utilities offered a small subset of the commands in use today with later versions of `lpd` and LPRNG. Some of the options covered here are a result of the widespread use of the LPRNG printing package, but noting them as such would be tiresome and bring nothing to the goal of exam readiness.

Each command is shown with its syntax and various examples in the following sections, including any exam alerts to clue you in to what to expect.

### The lpd Daemon

The `lpd` daemon is the main process that oversees the printing programs and tasks. The daemon is located in `/usr/sbin` and referenced by a script in the `/etc/rc.d/init.d` directory for Red Hat and the `/etc/init.d` directory for Debian.

The syntax for `lpd` is:

```bash
lpd -option parameter
```

The `/etc/lpd.conf` file might be present for later versions of `lpd` (and LPRNG) to hold the default configuration parameters. This file is read before the `/etc/printcap` is read, and any conflicting parameter settings between the two take on the latest applied value, such as banner settings or the shell used for running the filters.

### Print Filters

Print filters are subcommands or filtering programs that help the `lpd` process and format submitted print jobs for the destination print device.

Typically, `lpd` and the `/etc/printcap` configuration reference any or all of three types of filters:

- **OF**—Output filters are used for banner generation, initialization, and the termination strings that are sent to the print device.
- **Data**—Uses a lowercase character to identify a file type and then loads the appropriate filter type defined in the `/etc/printcap` to process the data.
- **Pipe**—If a `printcap` device is noted by a pipe followed directly by a program name, such as `|someprog`, the device being printed to is the actual program noted, which then has access to the real print device.

Print filters come in many varieties, the most common being `apsfilter`, `magickfilter`, and Red Hat's `über-filter`. These filters are relatively complex, and thankfully the only knowledge needed on the exam at this level is that they exist, what their names are, and their locations on the system:

- `apsfilter`—Used mostly for converting print jobs to the PostScript format, its configuration files are in the `/etc/apsfilter` or `/usr/local/etc/apsfilter` directory.
- `magicfilter`—Very configurable, this filter uses the magic numbers contained in the print files, particularly the file type and formatting that can be detected.
- Red Hat’s `printtool`—This utility does several operations for you, taking the place of or organizing the processing of print jobs using the various other filter options.

### Printing with lpr

The `lpr` command is used almost exclusively to print on a Linux system, either from the command line or as the subcomponent of a graphical print routine such as a word processor. The alternative is to have the application directly call the functions the `lpr` command uses.

Print jobs submitted with `lpr` take the following form:

```
lpr -option value filename
```

### lpr Command Options

`lpr` offers a number of options with which to specify print jobs:

- `b`—Forces the submission of a literal job; no filtering is done.
- `k` and `#`—Followed by a numeric value, these cause multiple copies to be printed.
- `P`—Followed either by a space and a printer name or directly by a printer name, this option specifies the printer to be printed to.
- `V`—Makes the process more verbose, showing extra information in some cases about the print job.

Printing a job to the default queue is simple; you use the command shown here:

```
lpr file2print
```

To print to a specific printer, such as one that is not the default, you use the following command:

```
lpr -P hplaser file2print
```

Interestingly, you can leave out the space between the `-P` for the printer and the actual printer name itself, so the following command works identically to the previous example:

```
lpr -Phplaser file2print
```

To print more than one copy of a document, use the following command:

```
lpr -K3 file2print
```

This is identical to this command:

```
lpr -#3 file2print
```

> **ALERT:** Be aware that `lpr` accepts standard input like other commands, such as printing the contents of four files with the following command:
>
> ```bash
> cat file[1-4] | lpr -P hplaser
> ```
>
> This reads the contents of `file1`, `file2`, `file3`, and `file4` and then sends that output as a single print job to the printer `hplaser`.

### Monitoring Print Jobs with lpq

After you or others have submitted a print job to the queue, the `lpq` command is used to monitor the progress or status of those print jobs.

`lpq` is a read-only or informational tool; it cannot be used to alter anything about your machine’s printing configuration or do anything to the listed print jobs. Several other commands, which are covered next, are used for those tasks.

The `lpq` command syntax is as follows:

```
lpq -option value
```

### lpq Command Options

`lpq` offers several options to control how information is presented:

- `-a`—Used to specify that all print queues should be queried.
- `-P`—Followed by a value for the printer name, it’s used to specify a particular printer to query.
- `-l`—Used for verbose output.
- `-L`—Increases the verbosity of output to an alarming level, simulating debug information.
- `-t`—Followed by a value of seconds, this displays the specified queues, waits the length of the sleep time, and displays the queue's information again until it's interrupted by a Ctrl+C.

### Examples of Using lpq

`lpq` is usually the first utility you should run if you're not sure that printing is occurring properly. It gives you quick and precise information and can be used to troubleshoot if you use the `-l` option for increased verbosity.

To show the jobs in the default queue, use the command shown here:

```
lpq
```

This returns output similar to:

```
Printer:  hplaser@localhost
Queue: 1 printable job
Server: pid 23462 active
Unspoiler: pid 23463 active
Status: IF filter 'mf_wrapper' filter msg - '' at 14:39:13.726
Rank  Owner/ID    Class Job Files    Size Time
active  root@localhost+461  A  461 /etc/printcap 997 14:39:13
```

> **Note:** As you can see, a lot of information is already in an `lpq` query. I won't torture you (and the editorial staff) with the output from the most verbose options because it would fill a couple of pages.

To view a queue other than the default, such as the `brother` queue, use this command:

```
lpq -P brother
```

This produces this output:

```
Printer:  brother@localhost
Queue: no printable jobs in queue
Status: brother: Ready
```

Additionally, you can view all the print queues with either the `-a` or `-all` option, such as:

```
lpq -a
```

This returns output similar to:

```
Printer:  hplaser@localhost
Queue: no printable jobs in queue
Status: hplaser: Update_status: no identifier for 'hfA461' at 14:43:53.544
Printer: brother@localhost
```
