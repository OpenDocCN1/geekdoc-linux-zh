# 8.1 Event infrastructure 145

In order to determine which API revision the system should call conform to, the perf_event_attr.size field is to the size of the perf_event_attr structure. If a specific revision is desired, the field can be set to the corresponding size for that revision. These values are defined in the perf_event.h header file, the kind of PERF_ATTR_SIZE. For instance:

```
$ grep PERF_ATTR_SIZE_VER /usr/include/linux/perf_event.h
#define PERF_ATTR_SIZE_VER0 64 /* sizeof first published
    struct *; 
#define PERF_ATTR_SIZE_VER1 72 /* add: config2 */
#define PERF_ATTR_SIZE_VER2 80 /* add: branch_sample_type */
#define PERF_ATTR_SIZE_VER3 96 /* add: sample_regs_user */
```

Besides these, the other configuration options are fields within the structure. There are four fields that allow the exclusion of contexts: (0) perf_event_attr.exclude_user (1) perf_event_attr.exclude_kernel (2) perf_event_attr.exclude_hv.forhypervisor,(3) perf_event_attr.exclude_idle. There are three fields that control the monitoring of child processes, (0) perf_event_attr.inherit, which determines whether child processes should be included in the measures, (1) perf_event_attr.inherit_stat, which determines the counters are preserved between context switches to an inherited process, and (2) perf_event_attr.enable_on_exec, which automatically enables the counters after an exec(2), thus simplifying the task of monitoring another process.

The perf_event_attr.pinned field specifies that the event should always be enabled on the core. The perf_event_exclusive field specifies that the event, including its group, are the only events enabled on the processor. This is designed for handling events that interfere with other counters. The perf_event_attr.disabled field specifies that the event should be started, leaving the event to be selectively enabled when measurement is desired

The perf_event_attr.precise_ip allows for PEBS, in Chapter 6, to be enabled.

As previously mentioned, events can be counted and sampled. While counted events are accessed through read(2), samples are accessed via pages with mmap(2). The process of parsing the results will be covered more detail in Sections 8.1.5 and 8.1.6.

# Counted event configuration

Configuring counting events is straightforward. Unlike sampled events, there is really one counting-specific configuration option, perf_event_attr.read_format. This option controls what information is present in the buffer filled by the read(2) call.

There is no predefined struct in perf_event.h for the result's format. This is because the result's format is customizable. The fields whose associated flags aren't specified in perf_event_attr.read_format will be excluded. As a result, updating the perf_event_attr.read_format field without updating the associated code that