
## Table III. Detailed resource specifications

### Task: -a cpu:path

| Item | Details |
| :--- | :--- |
| **Explanation** | Assigns a CPU resource at a specific path (bound CPU) to the vPar's configuration. The CPU replaces a monitor-assigned bound CPU. Bound CPUs are able to process interrupts. |
| **Value** | A text string of the form returned by the `ioscan(1M)` command, such as “10/12/6” |
| **Usage Restrictions** | The vPar must not be running. This restriction may be removed in a future release.<br>The total number of CPUs at a specific path must be <= min<br>In addition, if the vPar is in the monitor database:<br>- A CPU must exist at path,<br>- It must be available (not assigned to a vPar, including the target vPar). |
| **Usage Guidelines** | The addition does not increase either the number of total CPUs or bound CPUs allocated to the vPar. Instead, it replaces a previously bound CPU whose path had been selected by the monitor. To increase total CPU allocation, specify an appropriate new `num`. To increase the number of bound CPUs, specify a new `min`.<br><br>Hewlett-Packard recommends that users configure specific CPUs only when required for performance reasons. In other situations, specify only the total number of CPUs (`num`) and how many of these should be bound (`min`), and allow the monitor to manage the actual CPUs allocated. |

### Task: -a cpu:num

| Item | Details |
| :--- | :--- |
| **Explanation** | Adds `num` unbound CPUs to the vPar's configuration. The CPUs are drawn from a systemwide pool of available CPUs. |
| **Value** | A positive integer |
| **Usage Restrictions** | If the vPar is in an alternate database file or is in the live monitor database but not running:<br>- Total number of CPUs <= max<br>In addition, if the vPar is running:<br>- `num` CPUs must exist on the system,<br>- They must have been available (not bound to any vPar) at the time the vPar was booted.<br>If another vPar is deleted with the `vparremove` command, its bound CPUs cannot be added as floaters to a running vPar. |

### Task: -a cpu:: [min] [:: [max]]

| Item | Details |
| :--- | :--- |
| **Explanation** | Specifies the minimum and maximum number of CPUs allowed for the vPar. This operation does not allocate any CPUs, but specifies the limits of other allocation tasks. |
| **Details** | Both `min` and `max` are optional. The default `min` is platform-dependent but is currently = 1. The default `max` is 32767 if creating a vPar in an alternate database. If creating a vPar in the monitor database, the default `max` is the total number of CPUs on the entire hardware system. |
| **Value** | If specified, `min` and `max` must be positive integers such that `min` < `max`. |
| **Usage Restrictions** | This option is allowed only in the `vparcreate` command.<br><br>`min` cannot exceed the total number of CPUs. The default total when the vPar is created is 1. Use the `-a cpu::num` option to change the total before setting a `min` other than 1.<br><br>`max` cannot be less than the total.<br><br>`min` cannot be less than the total number of CPUs configured by explicit path. |

### Task: -a iopath: [attr1] [,attr2]

| Item | Details |
| :--- | :--- |
| **Explanation** | Adds the I/O resource at `path` to the vPar.<br><br>If attributes are specified, they are associated with the resource. If the vPar already owns the resource, any specified attributes are added to its configuration.<br><br>This option only adds specified attributes. The state of unspecified attributes is not changed. |
| **Value** | `path`: A text string of the form returned by the `ioscan(1M)` command, such as "10/12/5"<br><br>`attr`: One or both of the case-insensitive attribute strings ALTBOOT and BOOT. If both are specified, they are separated by a comma (","), |
| **Usage Restrictions** | The vPar must not be running.<br><br>The I/O resource must either be unassigned or (when adding attributes to an already assigned resource) be assigned to the target vPar. |
| **Usage Guidelines** | At most one device can be assigned the ALTBOOT and BOOT attributes. Assigning one of these attributes to a device silently deletes it from its former device, if any.<br><br>Caution: You should assign attributes to appropriate devices, but this is not checked. For example, ALTBOOT and ROOT should be assigned to a disk or tape. Failure to do this may result in an unbootable partition. |

### Task: -a mem::size

| Item | Details |
| :--- | :--- |
| **Explanation** | Specifies the increase, in megabytes rounded upward to a 64 megabyte boundary, in the total amount of memory to be allocated to the VPar. This memory is taken from unspecified ranges of memory available to the system when the partition boots. |
| **Value** | A positive 64-bit integer <= 175921860444152 |
| **Usage Restrictions** | The vPar must not be running.<br><br>If the vPar is in the monitor database, this memory must physically exist and be available after the memory requirements of all other vPars have been satisfied.<br><br>If the vPar is in an alternate database file, the assignment always succeeds. The amount of memory actually allocated by the database is loaded into the monitor may be less if some or all of it is needed in other vPars. |

### Task: -a mem::base-range

| Item | Details |
| :--- | :--- |
| **Explanation** | Specifies an explicit address space of memory starting at `base` bytes and extending for `range` megabytes. Both quantities are rounded upward as required to be aligned on 64 megabyte boundaries. |
| **Values** | `Base`: An unsigned 64-bit integer <= 0xffffffffffffffff<br>`Range`: A positive 64-bit integer <= 175921860444152 |
| **Usage Restrictions** | The vPar must not be running.<br><br>No part of the range may be already owned by this or another vPar.<br><br>If the vPar is in the monitor database, the entire range must exist in the system.<br><br>The total memory allocated in specific ranges must not exceed the vPar's memory size specification. |
| **Usage Guidelines** | Addition of specific memory ranges does not increase the total amount of memory allocated to the vPar. Any such memory is a part of that total amount.<br><br>Caution: It is possible to specify memory ranges and sizes such that none of the vPars will launch. Hewlett-Packard recommends that users configure specific memory ranges only when required for performance reasons. In other situations, specify only total memory and allow the monitor to manage the actual ranges allocated. |

### Task: -m cpu::num

| Item | Details |
| :--- | :--- |
| **Explanation** | Sets the total number of CPUs (bound and unbound) to `num`. |
| **Value** | A positive integer |
| **Usage Restrictions** | If the vPar is in an alternate database file or is in the live monitor database but not running:<br>- `num` must be between `min` and `max`.<br><br>In addition, if the vPar is in the live monitor database and `num` increases the total:<br>- `num` CPUs must exist on the system.<br>- They must have been available (not bound to any vPar) at the time the vPar was booted.<br><br>If another vPar is deleted with the `vparremove` command, its bound CPUs cannot be added as floaters to a running vPar. |

### Task: -m cpu::[min] [; [max]]

| Item | Details |
| :--- | :--- |
| **Explanation** | Specifies the minimum and maximum number of CPUs allowed for the vPar. This operation does not allocate any CPUs, but specifies the limits of other allocation tasks.<br><br>You can change only `min` or `max` by not specifying the other field. |
| **Value** | If specified, `min` and `max` must be positive integers such that `min` <= `max`. |
| **Usage Restrictions** | The vPar must not be running.<br><br>`min` cannot exceed the total number of CPUs.<br><br>`max` cannot be less than the total.<br><br>`min` cannot be less than the total number of CPUs configured by explicit path. |

### Task: -m iopath[:attr1[,attr2]]

| Item | Details |
| :--- | :--- |
| **Explanation** | Changes the attributes of the resource to those specified in the option. Omitted attributes are removed from the attribute set. To retain an attribute, it must be specified. |
| **Value** | `path`: A text string of the form returned by the `ioscan(1M)` command, such as "/0/12/6"<br><br>`attr`: One or both of the case-insensitive attribute strings ALTROOT and ROOT. If both are specified, they are separated by a comma ",". |
