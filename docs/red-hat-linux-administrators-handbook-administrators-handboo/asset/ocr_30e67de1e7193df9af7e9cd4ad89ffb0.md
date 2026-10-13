Optionally, you can also specify command-line arguments for the process in the fourth field.

As mentioned before, a run level specifies a state of the system. The nine run levels are described in Table 2-1.

# Table 2-1 The Run Levels for init

| Run Level | Description |
|---|---|
| 0 | Halt – used to halt the system |
| 1 | Single-user – used to set the system in a minimal configuration suitable for a single user |
| 2 | Not used |
| 3 | Multiuser – used to set the system in a configuration that supports multiple users |
| 4 | Not used |
| 5 | Used to start X Window System and the xdm program |
| 6 | Reboot – used to reboot the system |
| S or s | Used internally by scripts that run in run level 1 |
| a, b, c | On-demand run levels; typically not used |

Note that you can specify multiple run levels in a single init configuration line. For example, if you want init to run a process for both single- and multiuser modes, you can specify a line such as the following:

```
id:13:action:process arguments
```

Table 2-2 shows the possible values for actions.

# Table 2-2 Possible Actions for a Specific Run Level

| Action | Description |
|---|---|
| respawn | The process is restarted whenever it terminates. |
| wait | The process is run once, and init waits until it terminates. |
| once | The process is run once. |
| boot | The process is run during system boot, and init ignores the run level field. |
| bootwait | The process is run during system boot, and init waits for the process to terminate. |