# # sysctl

**Purpose:** Display and edit kernel parameters on Linux and BSD systems.

**Usage syntax:** `sysctl [OPTIONS]`

```
$ sysctl -a
kernel.sched_shares_ratelimit = 500000
kernel.sched_shares_thresh = 4
kernel.sched_child_runs_first = 1
kernel.sched_features = 24191
kernel.sched_migration_cost = 500000
kernel.sched_nr_migrate = 32
kernel.sched_rt_period_us = 1000000
kernel.sched_rt_runtime_us = 950000
kernel.sched_compat_yield = 0
kernel.panic = 0
kernel.core_uses_pid = 0
kernel.core_pattern = core
...
```

![](bbox=[0.39, 0.42, 0.61, 0.43])

The `sysctl` command displays and edits tunable kernel parameters. This allows you to fine tune various aspects of the operating system.

> **Warning** *You should not change these values unless you fully understand the impact of the parameter you are setting.*

Kernel parameters are typically stored in the `/etc/sysctl.conf` file. Settings changed on the command line via `sysctl` will be lost at reboot unless they are added to the `sysctl.conf` file.

> **Note** *HP-UX and Solaris use the `sysdef` command in place of `sysctl`. AIX systems use the `tunchange` command.*

**Common usage examples:**

| `sysctl -a` | Display all kernel parameters |
| `sysctl -w [SETTING]=[VALUE]` | Set the specified kernel parameter |