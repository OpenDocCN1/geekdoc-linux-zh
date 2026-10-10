# Review Questions

+   11. The tar program provides a much easier \_\_\_\_\_\_\_\_ process than RPM and Debian package tools do.
+   A. dependency tracking
+   B. source code compilation
+   C. file ownership setting
+   D. package creation

+   12. What is wrong with the following commands, which are intended to record an incremental backup on a tape that already holds one incremental backup?
+   ```
+   # mt -f /dev/st0 fsf 1
+   # tar cvlpf /dev/st0 --listed-incremental /root/inc /home
+   ```
+   A. The mt command should terminate in 2, rather than 1, to skip to the second position on the tape.
+   B. When backing up /home, the incremental file must reside in /home, not in /root.
+   C. The device filename should be a nonrewinding name (such as /dev/nst0), not a rewinding name (/dev/st0).
+   D. The incremental backup must include the root (/) directory; it cannot include only /home.

+   13. What is an advantage of using rsync for network backups, as compared to FTP or NFS?
+   A. rsync can be used by any user.
+   B. rsync can reduce network bandwidth use.
+   C. rsync can back up across architectures (x86 to PowerPC, for instance).
+   D. rsync can back up from any filesystem type (XFS, ReiserFS, and so on).

+   14. Which of the following is a true statement concerning the ability to restore a backup used making Linux’s dump to a partition that’s formatted with XFS?
+   A. You must use cpio’s -H dump option to do the job.
+   B. You must use the dump utility’s -r option to do the job.
+   C. You must use the xfrestore utility to do the job.
+   D. This task cannot be directly and easily performed.

+   15. You need to restore some files that were accidentally deleted. Which of the following commands can be used to list the contents of an archive stored on a SCSI tape?
+   A. `cpio -itv > /dev/st0`
+   B. `cpio -otv > /dev/st0`
+   C. `cpio -otv < /dev/st0`
+   D. `cpio -itv < /dev/st0`