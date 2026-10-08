The following table shows the actions that result from specific combinations of tracing, enabling, and connecting.

| Enabled or Disabled | Tracing State (On/Off) | Debug State (Connected/Cleared) | Results in |
| --- | --- | --- | --- |
| Enabled | On | Connected | Tracing and debugging |
| Enabled | On | Cleared | Tracing only |
| Enabled | Off | Cleared | Debugging only |
| Enabled | Off | Connected | Nothing |
| Disabled | On | Cleared | Nothing |
| Disabled | On | Connected | Nothing |
| Disabled | Off | Cleared | Nothing |
| Disabled | Off | Cleared | Nothing |

# List History # list probes control command history

The list history command displays a list of the probe control commands previously issued in the tracing session, for example, connect, clear, trace, disable. Commands in the history list are executed whenever a new shared object is brought into the target program by diopen(3DL).

# Commands to List Probes or List Values

```
list spec_list $set_name      # list probes all
list spec_list selector_list # list name probes
                             # file=test.c
list values spec_list          # list values keys
list tracefile                # list tracefile
```

The two commands list the selected attributes and values of the specified probes. You can use them to check the state of a probe. The third command lists the various values associated with the selected attributes. The fourth command lists the current datafile.

# Help Command

help topic

Invoke the help command with no arguments to view a list of the available topics. If a topic argument is specified, help is printed for that topic.

# Source a File

```
source filename
```

You can use the source command to source a file of pre commands. source can be nested (that is, a file can source another file).