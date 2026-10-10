# jobs

**Purpose:** Display background and suspended jobs.

**Usage syntax:** `jobs [OPTIONS]`

```
$ jobs  
[1]-  Running        SomeProgram.sh  
[2]+  Stopped        AnotherProgram.sh  
[3]   Stopped        Test.sh
```

Displaying background programs using the jobs command

The `jobs` command displays the status of background programs and suspended processes. In the above example, three background jobs are displayed. The previously mentioned `fg` and `bg` commands can be used to move the processes to the foreground and background respectively.

The following table describes the output fields of the `jobs` command.

| Job ID | Status | Program |
| :-- | :-- | :-- |
| `[1]-` | Running | `SomeProgram.sh` |
| `[2]+` | Stopped | `AnotherProgram.sh` |
| `[3]` | Stopped | `Test.sh` |

Output fields of the jobs command

> **Note**  
> *The plus sign is used to indicate what job is considered to be the default job (for use with the `bg` and `fg` commands). The minus sign indicates the job that will become the default if the current default job terminates. There can be only one + or - at any given time. All other jobs will not have any indicators.*

**Common usage examples:**

`jobs` Display all jobs

`jobs -1` Display all jobs and their PID