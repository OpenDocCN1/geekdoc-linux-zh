# 176 CHAPTER 9 Ftrace

+   17 nvi-5859 [001] d... 610.322073: 8.0 D WS 78752176 + 32 [nvi]
18 <idle>-0 [006] d. 610.322628: 8.0 C WS 78752176 + 32 [0]

# LISTING 9.3

Modified output snippet of the blk tracer in the trace file.

# Nop

nop tracer is the default. As the name implies, this tracer doesn't trace anything; however, it can be used to collect tracepoint events.

Each static event can be searched, enabled, or disabled via the tracing/events directory. Within this directory are additional directories representing kernel subsystem that exposes events. Within each of these subdirectories, each representing a specific event. At each of these levels, there are entries enable, which are available to enable or disable all events within the subdirectories.

```
# pwd
/sys/kernel/debug/tracing
# cat set_event
# echo "*1915:*" > set_event
# cat set_event | head -n 5
1915:1915_pipe_update_start
1915:1915_pipe_update_vblank_evaded
1915:1915_pipe_update_end
1915:1915_gem_object_create
1915:1915_vma_bind
# echo "*\!1915:*" > set_event
# cat set_event
```

By monitoring these events, it is possible to correlate the behavior of user space applications to kernel behavior.

# 9.2 KERNEL SHARK

While the DebugFS interface to Ftrace is very flexible, requires no special tools, and can be easily integrated into an application, there are two other interfaces available. The, trace-cmd, is a command-line tool that wraps the DebugFS