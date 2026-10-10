# —reverse

Show reverse dependencies between units with **list-dependencies**, i.e. follow dependencies of type *WantedBy=* , *RequiredBy=* , *RequiredByOverridable=* , *PartOf=* ,  
*BoundBy=* , instead of *Wants=* and similar.

# —after

With **list-dependencies**, show the units that are ordered before the specified unit. In other words, recursively list units following the *After=* dependency.

Note that any *After=* dependency is automatically mirrored to create a *Before=* dependency. Temporal dependencies may be specified explicitly, but are also created implicitly for units which are *WantedBy=* = targets (see \(5\)), and as a result of other directives (for example *RequiresMountsFor=* ). Both explicitly and implicitly introduced dependencies are shown with **list-dependencies**.

# —before

With **list-dependencies**, show the units that are ordered after the specified unit. In other words, recursively list units following the *Before=* dependency.

# -l, —full

Do not ellipsize unit nas, process tree entries, journal output, or truncate unit descriptions in the output of **status**, **list-units**, **list-jobs**, and **list-timers**.

# —show-types

When showing sockets, show the type of the socket.

# —job-mode=

When queueing a new job, this option controls how to deal with already queued jobs. It takes one of “fail”, “replace”, “replace-irreversibly”, “isolate”, “ignore-dependencies”, “ignore-requirments” or “flush”. Defaults to “replace”, except when the **isolate** command is used which implies the “isolate” job mode.

If “fail” is specified and a requested operation conflicts with a pending job (more specifically: causes an already pending start job to be reversed into a stop job or vice versa), cause the operation to fail.

If “replace” (the default) is specified, any conflicting pending job will be replaced, as necessary.

If “replace-irreversibly” is specified, operate like “replace”, but also mark the new jobs as irreversible. This prevents future conflicting transactions from replacing these jobs (or even being enqueued while the irreversible jobs are still pending).