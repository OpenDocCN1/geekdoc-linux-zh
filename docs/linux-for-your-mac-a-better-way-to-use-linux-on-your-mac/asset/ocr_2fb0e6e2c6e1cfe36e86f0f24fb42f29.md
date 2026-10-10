+   * What kind of back up equipment is already on hand?
+   * What procedure is currently in place?
+   * When was the last archive made of the system?
+   * When was the last backup made of the system?
+   * When was the last system failure and what caused it?

Obviously no one ever wants to ever lose data a single document, program, or multimedia file. Is this always possible? The answer is yes, if you take all the necessary precautions, devise a good back up plan, and have adequate equipment. Fortunately, since you use Linux, you also have the necessary software tools.

Some hardware solutions, such as RAID (*Redundant Array of Inexpensive Disks*), can provide an initial measure of security, but it is best to devise a schedule that can cover any loss of data and still have a backup in place. For example, an incremental backup strategy is extremely beneficial and can shorten the time required for back-ups, as the operation saves only those files that have changed since the last backup.

One approach, using two sets of media is:

+   * **Sunday.** Back up the entire system
+   * **Monday through Saturday.** Back up all changed files

Another approach, requiring seven sets of media is:

+   * **Sunday.** Back up entire system
+   * **Monday through Saturday.** Back up all changed files from the previous day

Yet another more comprehensive approach is:

+   * **Sunday.** Back up the entire system
+   * **Monday through Saturday.** Back up all files changed from the previous day
+   * **Following Sunday.** Backup all files changed from previous week
+   * **Following three weeks.** Backups are repeated and the process is started over

Choosing an economical backup medium can also be a crucial factor. However, due to the low prices of CD-Rs, high-speed and high capacity tape drives, and the continual dropping cost of hard drive storage, many administrators are choosing one of these media.

# ### Using the gzip Command

The GNU `gzip` command is a compression and decompression utility similar to Stuffit. However, `gzip` does not have the ability to save the resource fork used by