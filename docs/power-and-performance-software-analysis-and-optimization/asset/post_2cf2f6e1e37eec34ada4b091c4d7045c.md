
## 8.1 Event infrastructure

a struct, perf_event_attr, is populated. This struct describes the event to be collected, how the measurements should occur, and how the results should be reported. The system call returns a file descriptor that is utilized for accessing the data collected. In other words, this system call is invoked for each event to be monitored.

At the time of this writing, no wrapper exists for this system call in glibc, and manually, for instance, with the `SYSCALL` instruction. The function prototype can be found in Listing 8.1.

```c
int perf_event_open(struct perf_event_attr *attr, pid_t pid,
               int group_fd, unsigned long flags);
```

LISTING 8.1
perf_event_open(2) function prototype.

As mentioned above, the attr argument is responsible for communicating the event configuration.

The pid specifies the process to monitor. A pid of 0 measures all processes on the system, and a positive pid measures the process with the given pid.

The cpu argument specifies the logical processor to monitor. A cpu value of -1 monitors all logical processors, with a positive or zero value limits collection to the specified processor.

The group_fd argument is the file descriptor of the group leader. This allows for multiple events to be grouped together. An event group is only scheduled to be collected when all members are available to be measured. Thus, all events that will be calculated or compared should be members of the same group, ensuring that each metric is computed based on simple code execution. The first event, the leader, is created with a group_fd of -1. The file descriptor returned for the leader is then passed as the value for group_fd during the creation of all other events in the group.

Finally, the flags argument allows for specifying any behavioral modifiers. Currently, the only flag the author sees of value is PER_FLAG_PID_CGROUP, which allows for system-wide monitoring to a cgroup.

The perf_event_open(2) function follows the standard conventions for a function that opens a file descriptor, that is, returning the new file descriptor or -1 and setting errno.

## 8.1.2 SELECTING AN EVENT

Events are selected by populating the perf_event_attr structure and then passing it to the kernel. This data structure, as expected by the kernel ABI, is defined in /usr/include/linux/perf_event.h. This header file also includes the enumerations for the various events, as well as any other ABI definitions.

Due to the flexibility of the interface, the event attribute structure is fairly complex. Determining which fields to populate in this structure depends on the desired information.

The first step is to select the event and event type, corresponding to the perf_event_attr.config and perf_event_attr.type fields, respectively. At the time of this writing, the following predefined event types are listed in the perf_event.h header file:

```
PERF_TYPE_HARDWARE Hardware Event
PERF_TYPE_SOFTWARE Software Event
PERF_TYPE_TRACEPOINT Tracing Event
PERF_TYPE_HW_CACHE Hardware Cache Event
PERF_TYPE_RAW Hardware Event
PERF_TYPE_BREAKPOINT Hardware Breakpoint
```

Additionally, the supported events and event types can be enumerated by sysfs. The event types can be iterated via the event_source base in sysfs. Each directory in /sys/bus/event_source/devices/ represents an event type. To select that event, use the perf_event_attr.type field to find the value in that corresponding directory's type file. Notice that the values exported by sysfs corresponds with the predefined values. For instance:

```bash
$ ls /sys/bus/event_source/devices/
breakpoint@ cpu@ power@ software@ tracepoint
$ cat /sys/bus/event_source/devices/software/type
1
$ grep PERF_TYPE_SOFTWARE /usr/include/linux/perf_event.h
```

```bash
PERF_TYPE_SOFTWARE = 1.
$ cat /sys/bus/event_source/devices/power/type
6
```

Each of these events has a corresponding directory in /sys/devices. Within some of these directories are an events subdirectory. Within this events directory is a file for each predefined event. These predefined event files contain the necessary information to program the event. For example:

```bash
$ ls /sys/devices/cpu/events
Branch-instructions cache-misses instructions
Ref-cycles branch-misses cache-references
Mem-loads stalled-backend bus-cycles
cpu-cycles mem-stores stalled-cycles-frontend
$ cat /sys/devices/cpu/events/cpu-cycles
event=0x3c
$ cat /sys/devices/cpu/events/ref-cycles
event=0x03
$ ls /sys/devices/power/events
```

energy-cores energy-gpu energy-pkg
energy-cores.scale energy-gpu.scale energy-pkg.scale
energy-cores.unit energy-gpu.unit energy-pkg.unit

Notice in the above example, an event type named “power” was available; however, this event type was not present in the list of ABI event types. This is because, at the time of this writing, the ABI header doesn't have a corresponding entry in the perf_type_id for this type. The “power” event type, introduced less than a year ago, adds events that utilize the RAPL interface, described in Section 3.2.4, to provide power consumption information. This illustrates how the infrastructure is evolving. Andi Kleen has written a library, libevents, to parse the events listed in it. It is available at https://github.com/andikleen/pmu-tools/tree/master/events

## PERF_TYPE_HARDWARE

When perf_type_attr is set to PERF_TYPE_HARDWARE, the contents of perf_event_attr are interpreted as one of the predefined processor events. Some of these events and their meanings are listed in Table 8.2. The exact PMU counter representing each of these events can be determined by searching for the event name in the $LINUX_SRC/arch/x86/kernel/ directory. This information can be cross-referenced with Volume 3, Chapter 19 of the Intel® Software Developer Manual to determine the precise mechanism.

As mentioned in the introduction, abstract PMU events is challenging. The majority of events are nonarchitectural, their behavior can vary from one processor architecture to the next. As a result, defining events for every available event would clutter the API with thousands of events that are only useful on a specific platform. Thus, most PMU events are only accessible with the PERF_TYPE_RAW event type.

Another challenge with the predefined events is that there is no guarantee that these events will continue measuring the same counts in future kernel versions. In summary, the predefined events of type PERF_TYPE_HARDWARE are convenient for basic PMU usage. For more serious performance work, it is better to use the PERF_TYPE_RAW events and specify the counts directly.

## PERF_TYPE_RAW

The interpretation of perf_event_attr config when perf_event_attr is set to PERF_TYPE_RAW depends on the architecture. For Intel® platforms, the format of the programmable PMU MSR, shown in Figure 6.1. Of these bits, only the ones that identify the event are required. The kernel automatically sets the other bits based on the other attributes in the perf_event_attr struct. For example, the OS and US fields are set on depends on the values of perf_event_attr.exclude_kernel and perf_event_attr.exclude_user. In other words, only the umask and event number need to be set for most events. Some events may also require setting the cmask, inverse, or edge detect fields. The information for each event is listed in Volume 3, Chapter 19 of the Intel Software Developer Manual.

### Table 8.2 Architectural Events of Type PERF_TYPE_HARDWARE
(Kleen et al., 2014)

| Event | Meaning |
| --- | --- |
| PERF_COUNT_HW_CPU_CYCLES | Unhalted Core Cycles. This counter only increments when the core is in C0 and not halted. Affected by changes in clock frequency. |
| PERF_COUNT_HW_INSTRUCTIONS | Instructions Retired. This counter increments when the last uop of an instruction is retired. Only incremented once for an instruction with a REP prefix. |
| PERF_COUNT_HW_CACHE_REFERENCES | LLC Reference. |
| PERF_COUNT_HW_CACHE_MISSES | LLC Miss. |
| PERF_COUNT_HW_BRANCH_INSTRUCTIONS | Branch Instruction At Retirement. Due to PMU skid, the flagged instruction during sampling is typically the first instruction of the taken branch. |
| PERF_COUNT_HW_BRANCH_MISSES | Mispredicted Branch at Retirement. Due to PMU skid, the flagged instruction during sampling is typically the first instruction of the taken branch. |
| PERF_COUNT_HW_BUS_CYCLES | Unhalted Reference. Unhalted Core Cycles, this counter increments at a fixed frequency. |
| PERF_COUNT_HW_REF_CPU_CYCLES | This event currently uses Fixed-Function events rather than the programmable events. Similar to BUS_CYCLES, this counter increments at a fixed rate, irrespective of frequency. Since the event code in the kernel assumes programmable events, the event code and umask coded in the config are bogus. |

Additionally, PMU events also require configuring other MSRs. Within the kernel, partitioned by generation process, of these events and the MSRs they utilize. When one of these events is selected, the contents of `perf_attr.config1` and `perf_attr.config2` are loaded into the extra MSRs. Since these registers vary depending on the event, the format will be specific to the event. Obviously for this work, the event must be properly configured within the kernel's PMU lists. These lists, arrays of `struct extra_reg`, can be found in `$[LINUX_SRC]/arch/x86/kernel/cpu/perf_event_intel.c`.
