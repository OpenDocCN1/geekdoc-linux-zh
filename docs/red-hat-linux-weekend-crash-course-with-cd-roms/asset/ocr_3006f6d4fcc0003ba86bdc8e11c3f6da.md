The fields have the following meanings:

+   - The *id* field is a unique, one- or two-character identifier. The *init* process uses this field internally. You can use any identifier you want as long as you do not use the same identifier on more than one line. For example, *si*, *x*, and *1* are all valid identifiers.
+   - The *runlevels* field is a sequence of zero or more characters, each denoting a run level. The line with the identifier *1*, for example, applies to run levels 1 through 5, so the *runlevels* field for this entry is 12345. This field is ignored if the *action* field is set to *sysinit*, *boot*, or *bootwait*.
+   - The *action* field tells the *init* process what to do with that specific entry. If this field is *initdefault*, for example, *init* interprets the *runlevels* field as the default run level. If this field is set to *wait*, *init* starts the process specified in the *process* field and waits until that process exits. Table 22-1 summarizes the valid action values you can use in the *action* field.
+   - The *process* field specifies the process that *init* has to start. Of course, some settings of the *action* field require no process field. (When *action* is set to *initdefault*, for example, no need exists for a *process* field.)

Table 22-1
Valid Actions in /etc/inittab

| Action | Description |
|---|---|
| respawn | Restarts the process whenever it terminates. |
| wait | Restarts the process once at the specified run level; *init* waits until that process exits. |
| once | Executes the process once at the specified run level. |
| boot | Executes the process as the system boots, regardless of the run level (the *runlevels* field is ignored). |
| bootwait | Executes the process as the system boots; *init* waits for the process to exit (the *runlevels* field is ignored). |
| off | Nothing happens for this action. |