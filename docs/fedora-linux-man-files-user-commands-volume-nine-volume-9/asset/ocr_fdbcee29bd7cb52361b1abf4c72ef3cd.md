# PROCESS SELECTION BY LIST

These options accept a single argument in the form of a blank-separated or comma-separated list. They can be used multiple tis. For example: `ps-p"12"-p3,4`

+   - -pid123
+       - Identical to `—pid123`.

+   - pid123
+       - Identical to `—pid123`.

+   - -Ccndlist
+       - Select by command na. This selects the processes whose executable na is given in *cmndlist*.

+   - -Ggrplist
+       - Select by real group ID (RGID) or na. This selects the processes whose real group na or ID is in the *grplist* list. The real group ID identifies the group of the user who created the process, see (2).

+   - -ggrplist
+       - Select by session OR by effective group na. Selection by session is specified by many standards, but selection by effective group is the logical behavior that several other operating systems use. This **ps** will select by session when the list is completely nuric (as sessions are). Group ID nuers will work only when so group nas are also specified. See the *-s* and *—group* options.

+   - —Groupgrplist
+       - Select by real group ID (RGID) or na. Identical to *-G*.

+   - —groupgrplist
+       - Select by effective group ID (EGID) or na. This selects the processes whose effective group na or ID is in *grplist*. The effective group ID describes the group whose file access permissions are used by the process (see (2)). The **-g** option is often an alternative to *—group*.

+   - **ppidlist**
+       - Select by process ID. Identical to *-p* and *—pid*.

+   - -ppidlist
+       - Select by PID. This selects the processes whose process ID nuers appear in *pidlist*. Identical to *p* and *—pid*.

+   - —pidpidlist
+       - Select by processID. Identical to *-p* and *p*.

+   - —ppidppidlist
+       - Select by parent process ID. This selects the processes with a parent processID in *pidlist*. That is, it selects processes that are children of those listed in *pidlist*.

+   - **qpidlist**
+       - Select by process ID (quick mode). Identical to *-q* and *—quick-pid*.

+   - -qpidlist
+       - Select by PID (quick mode). This selects the processes whose process ID nuers appear in *pidlist*. With this option **ps** reads the necessary info only for the pids listed