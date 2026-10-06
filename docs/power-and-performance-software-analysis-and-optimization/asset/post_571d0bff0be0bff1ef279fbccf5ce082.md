
# 9.1 DebugFS 173

| Column | Value |
| --- | --- |
| 24 3) | 0.211 us |
| 25 3) | 0.190 us |
| 26 3) | 0.131 us |

```c
update_wall_time() {
  _raw_spin_lock_irqsave();
  ntp_tick_length();
  ntp_tick_length();
  ntp_tick_length();
  timekeeping_update.constprop.9() {
    update_vsyscall();
    notifier_raw_call_chain() {
      notifier_call_chain() {
        pvclock_gtod_notify [kvm];
      }
    }
  }
  _raw_spin_unlock_irqrestore();
}
```

| Column | Value |
| --- | --- |
| 28 3) | 0.125 us |
| 29 3) | |
| 30 3) | 0.697 us |
| 31 3) | |
| 32 3) | | |
| 33 3) | 0.361 us |
| 34 3) | 2.347 us |
| 35 3) | 3.426 us |
| 36 3) | 6.415 us |
| 37 3) | 0.140 us |
| 38 3) | + 14.340 us |
| 39 3) | + 19.742 us |
| 40 3) | 0.115 us |
| 41 3) | + 28.784 us |

# LISTING 9.2

Output snippet of the *function_graph* tracer in the *trace* file.

# blk

The *blk* tracer records I/O requests at the block level. In order to utilize this, it is first necessary to select which devices to monitor. Every block device has a corresponding directory in sysfs at /sys/block/. Each of these directories is a *trace* directory, containing files that control if and how the device operations are traced. In order to enable tracing for a device, write "1" to the *enable* file in that directory. For example, in order to enable tracing for block device *sda*:

```bash
# echo 1 > /sys/block/sda/trace/enable
```

Once the device, or devices, have been selected for tracing, the tracer can be used like the others. Unlike the function tracer, the *blk* tracer doesn't print a header, so little is required in the format used. Starting at the far left, the first column contains the process name and pid. The second column consists of four distinct characters, starting from the left, indicates whether interrupts were enabled, whether the task needed to be rescheduled, whether the request occurred due to a software interrupt, hardware interrupt, or neither, and the preemption depth. The fourth column contains the absolute timestamp of the entry. Notice that to this point, these first four columns mirror the first fields of the *function* tracer.

The similarities end at the fifth column, which includes the major and minor device numbers for the block device. The sixth column summarizes what action in the block layer the entry represents. These values translate a trace action, blktr_act as defined in the $|LINUX_SRC|include/uapi/linux/blktr_api.h header as an ASCII character. Table 9.1 lists the values and their meanings. In the case this field contains an additional value, not listed in Table 9.1, follow the citations, which point to the source code and define and explain possible value.

Whereas the sixth column describes the action performed at the block layer, the seventh column describes the actual I/O operation. These values are much straightforward, with “W” standing for a write, with “R” standing for a read, with “S” standing for a sync, and so on. Finally, the eighth column provides the details of the operation, which depends on the action being.

# Table 9.1 Encodings of blk Trace Entry Actions (Howells, 2012; Rosted et al., 2009, b)

| Encoding | Action | Meaning |
| --- | --- | --- |
| Q | __BLK_TA_QUEUE | I/O request added to queue |
| M | __BLK_TA_BACKMERGE | I/O request merged into an existing operation (at the end) |
| F | __BLK_TA_FRONTMERGE | I/O request merged into an existing operation (at the front) |
| G | __BLK_TA_GETRQ | Allocate a request in the queue |
| S | __BLK_TA_SLEEPQ | Process blocked awaiting request allocation |
| R | __BLK_TA_REQUEUE | Request was not completed and is placed back onto the queue |
| D | __BLK_TA_ISSUE | Request entry issued to device driver |
| C | __BLK_TA_COMPLETE | I/O request complete |
| P | __BLK_TA_PLUG | Request entry in key awaiting more requests to improve throughput of block device |
| U | __BLK_TA_UNPLUG_IO | Plugged request has been released to be issued to device driver |
| I | __BLK_TA_INSERT | Request inserted into run queue |
| X | __BLK_TA_SPLIT | Request needed to be split into two separate requests due to a hardware limitation |
| B | __BLK_TA_BOUNCE | A hardware limitation prevented data from being transferred from the block device to memory, a buffer was used (which requires data copying) |
| A | __BLK_TA_REMAP | Request mapped to the raw block |

# 9.1 DebugFS 175

For example, Listing 9.3 contains a fragment of a blk trace. This trace records I/O operations by saving the file to the disk. Starting at line 3, the "WS" entry in column indicates that a write and sync operation are performed. The value of "A" in column six shows that this operation is BLK_TA_REMAP, the partition and file offset to a physical sector on the hard drive. The author's folder, which stores the file of interest, is in the third partition, as shown by the "8,3" major and minor numbers in the last column. The mapping operation of this entry completes, providing physical disk sector of 787216, and block offset 3. Moving to line 4, the write and sync operation continues by enqueuing the I/O request, hence the "Q" in sixth column. The enqueuing operation requests space be allocated to the host entry, hence the "G" in the sixth column, indicates that the request will be the hosting, waiting for additional requests to the same device. Starting on line 7

```
# tracer: blk
```

| Trace | Timestamp | Details |
| --- | --- | --- |
| nvi-5589 [001] d... | 610.322017 | 8.0 A 7872516 + 32 <-(8,3) 7316528 |
| nvi-5589 [001] d... | 610.322023 | 8.0 Q 7872516 + 32 [nvi] |
| nvi-5589 [001] d... | 610.322032 | 8.0 G 7872516 + 32 [nvi] |
| nvi-5589 [001] d... | 610.322035 | 8.0 P [nvi] |
| nvi-5589 [001] d... | 610.322042 | 8.0 I 7872516 + 32 [nvi] |
| nvi-5589 [001] d... | 610.322050 | 8.0 m ncfg5589SN / insert_request |
| nvi-5589 [001] d... | 610.322053 | 8.0 m ncfg5589SN / add_to_rr |
| nvi-5589 [001] d... | 610.322057 | 8.0 U [nvi] |
| nvi-5589 [001] d... | 610.322060 | 8.0 m ncfq workload:100 |
| nvi-5589 [001] d... | 610.322062 | 8.0 m ncfg5589SN / set_at_wl_class:0 wl_type:1 |
| nvi-5589 [001] d... | 610.322066 | 8.0 m ncfg5589SN / fifo=(null) |
| nvi-5589 [001] d... | 610.322067 | 8.0 m ncfg5589SN / dispatch_insert dispatched a request |
| nvi-5589 [001] d... | 610.322070 | 8.0 m ncfg5589SN / activate request, drv=1 |
| + 17 nvi-5859 [001] d... | 610.322073 | 8.0 D WS 7872516 + 32 [nvi] |
| 18 <idle>-0 [006] d. | 610.322628 | 8.0 C WS 7872516 + 32 [0] |
```

# LISTING 9.3

Modified output snippet of the blk tracer in the trace file.

# Nop

nop tracer is the default. As the name implies, this tracer doesn't trace anything; however, it can be used to collect tracepoint events.

Each static event can be searched, enabled, or disabled via the tracing/events directory. Within this directory are additional directories representing kernel subsystem that exposes events. Within each of these subdirectories, each representing a specific event. At each of these levels, there are entries.

## CHAPTER 9 Ftrace

## 9.2 KERNEL SHARK

While the DebugFS interface is very flexible, requires no special tools, and can be easily integrated into an application, there are two other interfaces available. The trace-cmd, is a command-line tool that wraps the DebugFS. The second, kernelshark, is a graphical interface that wraps the trace-cmd tool.

The kernelshark tool provides a very intuitive interface for configuring trace recording. Data collection is configured by selecting the Capture item in the menubar, and selecting the Record menu item. This will open a dialog that lists all of the events in a hierarchical tree, that, in the same format as file system exposes them. In this dialog, the tracer is referred to as the execute plugin, and there is a box widget for choosing one of the available tracers. Actual data collection begins and ends by selecting the Run and Stop buttons on this dialog. After clicking the button, the report will be displayed.

The advantage of using a graphical interface like kernelshark is the reporting. Figure 9.1 illustrates an example report. Once the trace has been collected, a timeline shows the events, partitioned by logical CPUs, using the trace's timestamps. The bottom half of the screen is dedicated to displaying the raw trace data. It is possible to zoom out of an outline, by left-clicking and then dragging. Dragging to the right causes the timeline to zoom in on the selected region between the start and end points.

FIGURE 9.1

The graphical interface for kernelshark.
