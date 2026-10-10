| | |
| --- | --- |
| Errors | Provides command error messages |
| Environment | Describes environment variable(s) used |
| Files | Defines files used by command |
| Versions | Describes command version information |
| Conforming To | Provides standards followed |
| Notes | Describes additional helpful command material |
| Bugs | Provides the location to report found bugs |
| Example | Shows command use examples |
| Authors | Provides information on command developers |
| Copyright | Defines command code copyright status |
| See Also | Refers to similar available commands |


Not every command's man page has all the section names described in Table 3-1. Also, some commands have section names that are not listed in the conventional standard.

In a command's synopsis section, you can find out how the command should be entered at the shell prompt. Many commands use a basic pattern:

```
COMMAND-NAME [OPTION]... [ARGUMENT]...
```

In the command's pattern structure,

+   - COMMAND-NAME is the name of the command used to run the desired program.

+   - [ OPTION ] s are additional items added to modify the command's behavior. There are typically many OPTIONS (also called switches) you can add. The brackets ([]) indicate that OPTIONS are not required, and the three dots (...) show that you can use more than one OPTION at a time.

+   - [ ARGUMENT ] is typically an item you pass to the command to let the program know you want it to operate on that item. You can see that it too is not required due to the brackets, and you can pass multiple ARGUMENTS to the program.