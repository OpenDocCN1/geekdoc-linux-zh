# 8.1 Event infrastructure 141

energy-cores energy-gpu energy-pkg
energy-cores.scale energy-gpu.scale energy-pkg.scale
energy-cores.unit energy-gpu.unit energy-pkg.unit

Notice in the above example, an event type named “power” was available; however, this event type was not present in the list of ABI event types. This is because, at the time of this writing, the ABI header doesn't have a corresponding entry in the perf_type_id for this type. The “power” event type, introduced less than a year ago, adds events that utilize the RAPL interface, described in Section 3.2.4, to provide power consumption information. This illustrates how the infrastructure is evolving. Andi Kleen has written a library, libevents, to parse the events listed in it. It is available at https://github.com/andikleen/pmu-tools/tree/master/events

# PERF_TYPE_HARDWARE

When perf_type_attr is set to PERF_TYPE_HARDWARE, the contents of perf_event_attr are interpreted as one of the predefined processor events. Some of these events and their meanings are listed in Table 8.2. The exact PMU counter representing each of these events can be determined by searching for the event name in the $LINUX_SRC/arch/x86/kernel/ directory. This information can be cross-referenced with Volume 3, Chapter 19 of the Intel® Software Developer Manual to determine the precise mechanism.

As mentioned in the introduction, abstract PMU events is challenging. The majority of events are nonarchitectural, their behavior can vary from one processor architecture to the next. As a result, defining events for every available event would clutter the API with thousands of events that are only useful on a specific platform. Thus, most PMU events are only accessible with the PERF_TYPE_RAW event type.

Another challenge with the predefined events is that there is no guarantee that these events will continue measuring the same counts in future kernel versions. In summary, the predefined events of type PERF_TYPE_HARDWARE are convenient for basic PMU usage. For more serious performance work, it is better to use the PERF_TYPE_RAW events and specify the counts directly.

# PERF_TYPE_RAW

The interpretation of perf_event_attr config when perf_event_attr is set to PERF_TYPE_RAW depends on the architecture. For Intel® platforms, the format of the programmable PMU MSR, shown in Figure 6.1. Of these bits, only the ones that identify the event are required. The kernel automatically sets the other bits based on the other attributes in the perf_event_attr struct. For example, the OS and US fields are set on depends on the values of perf_event_attr.exclude_kernel and perf_event_attr.exclude_user. In other words, only the umask and event number need to be set for most events. Some events may also require setting the cmask, inverse, or edge detect fields. The information for each event is listed in Volume 3, Chapter 19 of the Intel Software Developer Manual.