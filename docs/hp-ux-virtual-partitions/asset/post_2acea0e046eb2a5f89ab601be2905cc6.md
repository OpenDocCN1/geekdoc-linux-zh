
## Usage Restrictions
The vPar must not be running.
The I/O resource must be assigned to the target vPar.
Only attributes may be modified.

## Usage Guidelines
At most one device can be assigned the ALTBOOT and ROOT attributes. Assigning one of these attributes to a device silently deletes it from its former device, if any.

**Caution:** You should assign attributes to appropriate devices, but this is not checked. For example, ALTBOOT and ROOT should be assigned to a disk or tape. Failure to do this may result in an unbootable partition.

### Task: -m mem=size

**Explanation**
Specifies the total amount of memory, in megabytes rounded upward to a 64 megabyte boundary, to be allocated to the vPar. Any memory in excess of that specifically allocated by base and range is taken from unspecified ranges of memory available to the system when the partition boots.

**Value**
A positive 64-bit integer < 17592186044352

**Usage Restrictions**
- The vPar must not be running.
- A decrease in total memory allocation must not result in a total less than that of all memory allocated in specific memory ranges.
- If the vPar is in the monitor database and the specification results in an increased memory allocation, the memory must physically exist and be available after the memory requirements of all other vPars have been satisfied.
- If the vPar is in an alternate database file and total memory is increased, the assignment always succeeds. The amount of memory actually allocated if the database is loaded into the monitor may be less if some or all of it is needed in other vPars.

### Task: -d cpu:path

**Explanation**
De-assigns the bound CPU at the specified hardware path from the vPar and replaces it with a bound CPU of the monitor’s choice. Depending on availability, this may be the same CPU that was de-assigned.

**Value**
A text string of the form returned by the toscan(1M) command, such as “10/12/6”

**Usage Restrictions**
- The vPar must not be running.
- The resource at the specified path must be a CPU resource.
- The vPar must own the resource.

**Usage Guidelines**
- The deletion does not reduce either the number of total CPUs or bound CPUs allocated to the vPar. Instead, it replaces the explicitly specified CPU with a bound CPU selected by the monitor. To reduce total CPU allocation, specify an appropriate new num. To reduce the number of bound CPUs, specify a new min.
- Hewlett-Packard recommends that users configure specific CPUs only when required for performance reasons. In other situations, specify only the total number of CPUs (num) and how many of these should be bound (min), and allow the monitor to manage the actual CPUs allocated.

### Task: -d cpu:num

**Explanation**
Deletes num CPUs from the vPar's total configuration.

**Value**
A positive integer.

**Usage Restrictions**
- The vPar must own at least num CPUs.
- The new total number of CPUs >= min

### Task: -d io:path[:attr1[,attr2]]

**Explanation**
Removes the specified attributes of the resource leaving any previously assigned attributes unchanged and the resource itself assigned to the vPar. If no attribute is specified, removes the resource and all its attributes.

**Value**
- path: A text string of the form returned by the ioscan(1M) command, such as “10/12/6”
- attr: One or both of the case-insensitive attribute strings ALTBOOT and BOOT. If both are specified, they are separated by a comma [“,”].

**Usage Restrictions**
- The vPar must not be running.
- The I/O resource must be assigned to the target vPar.

**Usage Guidelines**
- Deleting an attribute from an I/O device does not cause it to be assigned to another. You must do that in a separate option or command.
- At most one device can have assigned the ALTBOOT and BOOT attributes.
- **Caution:** You should assign attributes to appropriate devices, but this is not checked. For example, ALTBOOT and BOOT should be assigned to a disk or tape. Failure to do this may result in an unbootable partition.

### Task: -d mem::size

**Explanation**
Specifies the decrease, in megabytes rounded upward to a 64 megabyte boundary, in the amount of total memory allocated to the vPar.

**Value**
A positive 64-bit integer <= 175921860444152

**Usage Restrictions**
- The vPar must not be running.
- The vPar must own at least the specified amount (after rounding) of non-specific memory.
- The decrease must not result in a total less than that of all memory allocated in specific memory ranges.

### Task: -d mem::base::range

**Explanation**
De-assigns an explicit address space of memory starting at base bytes and extending for range megabytes. Both quantities are rounded upward as required to be aligned on 64 megabyte boundaries.

**Values**
- Base: An unsigned 64-bit integer <= 0xffffffffc00000
- Range: A positive 64-bit integer <= 17592186044352

**Usage Restrictions**
- The vPar must not be running.
- The vPar must own the entire range.
- Either the start or end point of the specified range must match the start or end point of an existing range.

**Usage Guidelines**
- De-assigning specific memory ranges does not decrease the total amount of memory allocated to the vPar.
- **Caution:** It is possible to specify memory ranges and sizes such that none of the vPars will launch. Hewlett-Packard recommends that users configure specific memory ranges only when required for performance reasons. In other situations, specify only total memory and allow the monitor to manage the actual ranges allocated.

### SEE ALSO

vparboot(1M), vparcreate(1M), vparcmd(1f)(1M), vparremove(1M), vparreset(1M), vparstatus(1M), partition(5).

# vpstatus - Displays virtual partition and available resources information

![](img/eff8b9287a5f38c5adf538f24aacf29e_1010_0.png)

vpstatus(1M)                                    vpstatus(M)

## NAME

vpstatus - display information about one or more virtual partitions.

## SYNOPSIS

vpstatus [-v | -M] [-p vp_name]... [-D db_file]
vpstatus -A [-M]
vpstatus -w
vpstatus -e
vpstatus -R [-p vp_name]

## DESCRIPTION

The various forms of the *vpstatus* command display:

-   * The attributes and hardware resources associated with one or more virtual partitions (vPars) in either summary (the default) or detailed format. The -w option presents the same data in machine-readable format.
-   * Resources currently available, that is, not assigned to any virtual partition. The -M option presents the same data in machine-readable format.
-   * The name of the current virtual partition, that is, the virtual partition from which the command is run.
-   * The virtual partition monitor's event log.
-   * Processor Information Module (PIM) data from the most recent resetting of a virtual partition.

Only a superuser can execute the *vpstatus* command.

If no arguments are supplied, *vpstatus* displays a summary format of all attributes and resources of all virtual partitions in the monitor database. One or more virtual partitions may be specified explicitly in order to restrict the output to information about the selected virtual partitions. The -D option lists similar information from an alternate database file, but with a major difference. See the description of the -D option for further details.

There are three major listing formats. The format chosen depends on command options and forms:

-   * The summary format lists name, attributes, and resource totals. It is displayed if neither the -v nor -M option is used.
-   * The detailed format lists name, attributes, and detailed resource assignments, one per line with annotative headings. The -v option produces this format.
-   * The machine readable format displays the same information as the detailed format, except that field descriptive headers are omitted, and the information is all on one line. Individual fields are separated from each other by four delimiters. These are all described below.

Three additional formats are provided for the -w, -e and -R options.

Information displayed by vpstatus included the following:

-   * The name of the virtual partition (limited to 30 characters in summary format)
-   * The state of the virtual partition, from the list below:
    -   Up: The virtual partition has notified the monitor that it is up. This is the normal state of a running virtual partition, however it does not necessarily mean that the virtual partition has completed its initialization and is fully operational.
    -   Down: The virtual partition is fully halted. This could be the result of a normal /etc/shutdown -h command, or a paraphereset of a partition with its autoboot attribute set to manual. It is also the initial state of a virtual partition immediately after the virtual partition monitor is started.
    -   Load: The monitor is loading the kernel image of the virtual partition. This state precedes the boot state.
    -   Boot: The virtual partition has been launched, but has not completely booted.
    -   Crash: The virtual partition is shutting down ungracefully (either a panic or a reset)
    -   Shut: The virtual partition is shutting down gracefully
    -   Hung: The virtual partition has stopped sending heartbeat messages to the monitor.
    -   N/A: The virtual partition is in an alternate database file, and so has no state.
-   * The static/dynamic resource attribute
-   * The auto/manual boot attribute
-   * The path to the kernel (limited to 25 characters in summary format)
-   * The boot options (limited to 5 characters in summary format)
-   * Summary or detailed CPU, I/O, and memory resource allocations

## Options

vpstatus recognizes the following command line options and arguments:

```
-P vp_name    Restricts the command display to information about vp_name. By default, information about all virtual partitions in the monitor database or specified alternate partition database is displayed. Multiple vp_names may be specified, except when used to display PIM data.
```

```
-D db_file   Displays information from the alternate partition database file db_file rather than from the monitor
```
