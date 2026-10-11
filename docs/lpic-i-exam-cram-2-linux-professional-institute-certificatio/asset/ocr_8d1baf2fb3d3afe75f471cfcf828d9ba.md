The first column is the ID—in this case, it should be the numeral associated with the tty being configured for system accounting purposes, but it could be almost any number.

The second column is the runlevels in which this command or service is allowed to run or for which the program should take action in.

The third column is the action that should be taken for this entry; the possibilities are shown in the section following this one.

The fourth column is the command or service to be affected or run, along with any options and arguments needed.

Important values for the action column are

+   * `respawn`—This restarts the process when it’s terminated; it’s used mostly for X and login mingettys or gettys.

+   * `sysinit`—This is run before the default runlevel is entered.

+   * `initdefault`—This one sets the default runlevel.

+   * `ondemand`—Entries with this action can be invoked with an `init` command and options `a`, `b`, or `c`. No runlevel change happens—just the invoking of the configured program.

+   * `once`—This causes entries to be invoked only one time when the noted runlevels are entered.

+   * `wait`—This action is for processes that must be completed before anything else can happen, usually at the beginning of the entry into the runlevel. Then `init` continues.

The system’s default system runlevel entry lets the system know to which runlevel you want it to jump when the `sysinit` scripts are finished. This entry is important because the system defaults to this runlevel anytime the system is booted or rebooted. Any entry to have the system boot by default into a mode that features full multiple-user and networking capabilities but that presents a text-mode login would be as follows:

```
```bash
id:3:initdefault:
```
```

The system initialization entry sets the script or program that is run upon system initialization and before the default runlevel is reached. Notice there are no runlevels for this entry; they occur later:

```
```bash
si::sysinit:/etc/rc.d/rc.sysinit
```
```