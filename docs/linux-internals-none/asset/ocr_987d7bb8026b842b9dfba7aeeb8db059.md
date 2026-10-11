```
if (flags & CLONE_PID)
return current->pid;
```

returns the same PID immediately.

Once the last_pid has wrapped around the numbering space for PID (32,767), the code above starts looking for new PIDs. It will, however, jump to the next number after 300, because most numbers below 300 are usually taken by system daemons and programs started at boot and continuing run for the full life of the system. Those PIDs are hardly ever returned to the free list. To gain a few precious ticks, the kernel just skips them.

On a system configured for a maximum number of tasks beyond 32,767, it might theoretically occur that no PID slots are available. The task creation would therefore fail with a negative return code.

Obviously, the programmer does not always want to launch a copy of the original program, but rather wants to launch a totally different program at some point during program execution. For these cases, she must use exec().

The only way for a user program to pass execution to another program is to

+   1. Fork to another instance of itself using fork().
+   2. Then load another binary program image and pass execution to it using exec().

The kernel to implement the exec() call is in linux/fs/exec.c. The program is too long to be included here (almost a thousand lines in 2.3.52). Here is what it does upon being called:

+   1. The code for prepare_binprm() locates the file with the binary image and reads the first 128 bytes into the buf variable of brpm structure. (See the data structure at the end of this chapter.)

```
int prepare_binprm(struct linux_binprm *bprm)
{
int mode;
int retwal,id_change,cap_raised;
struct inode * inode = bprm->dentry->d_inode;

mode = inode->i_mode;
if (!S_ISREG(mode)) /* must be regular file */
return -EACCES;
if (!(mode & 0111)) /* with at least one_ execute bit set */
return -EACCES;
if (IS_NOEXEC(inode)) /* FS mustn't be mounted noexec */
```