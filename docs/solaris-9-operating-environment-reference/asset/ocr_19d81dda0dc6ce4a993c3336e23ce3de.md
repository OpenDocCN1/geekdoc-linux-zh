prctl — Get or Set the Resource Controls of Running
Processes, Tasks, and Projects

# Synopsis

```
/bin/prctl -t [basic | privileged system]] -e -d action [-rx]
-n name [-v value] [-i idtype] [id...]
```

# Description

Use the prctl command, new in the Solaris 9 Operating Environment, to examine and
modify the resource controls associated with an active process, task, or project on
system. prctl enables access to the basic and privileged limits on the specified entity.

# Options

+   -d | -e action
Disable (-d) or enable (-e) the specified action on the specified resource
control. The special token all is valid with the disable option to
deactivate all actions on the given resource control value.
The other defined actions for a resource are deny and signal=signum
deny action indicates that the resource control encountered tries to
deny granting the resource to the process, task, or project on a request
for resources in excess of the value provided by the -v option for the new
resource control. In the signal=signum action, signum is a signal
number (or string representation of a signal). You cannot activate or
deactivate deny actions when global flags indicate that the deny action
ununchangeable.

+   -i idtype Specify the type of the ID operands. Valid idtypes are process, task,
or project. The default ID type is process.

+   -n name Specify the name of the resource control to get or set. If you do not
spec name, prctl retrieves all resource controls.

+   -r Replace the first resource control value (matching with the -t privilege)
with the new value specified by the -v option.

+   -t [basic | system] Specify which resource control type to set. Unless the "lowerable" flag
is set for a resource control, only invocations by users (or root groups)
who have privileges equivalent to that of root can modify privileged
resource controls. See rctlblk_set_value(3C) for a description of the
RCTL_GLOBAL_LOWERABLE flag. If you do not specify the type, basic is
asumed. For a get operation, the values of all resource control types,
including system, are displayed if you specify no type.

+   -v value Specify the value for the resource control for a set operation. If you
specify no value, then the modification (deletion, action enabling or
disabling) is carried out on the lowest-valued resource control with the
type type.