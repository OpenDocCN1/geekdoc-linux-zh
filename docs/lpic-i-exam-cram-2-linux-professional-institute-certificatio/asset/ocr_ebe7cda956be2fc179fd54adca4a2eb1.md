# # Sample Choose Two/Three Question

Which steps must be performed before a newly installed hard drive is available for use by a normal user account? (Choose three.)

+   - A. mkfs
+   - B. mount
+   - C. scsi_info
+   - D. dd
+   - E. fdisk

Answers A, B, and E are correct. For a disk to be used by a standard or normal user, it must have at least one partition put on it (fdisk), have a file system of some type on that partition (mkfs), and be mounted by the root user or an entry in the /etc/fstab file that enables users to mount it without the root user's help. Answer C is incorrect because the scsi_info tool gathers information about SCSI devices but is not necessary to the process of a user gaining access to a disk. Answer D is incorrect because the dd command transfers one file format to another but has no effect on users accessing disks.

# # Choose All That Apply Questions

More difficult than the previous types, these actually make you think through all the possible answers because any of them might be right. LPI is the only vendor to my knowledge that uses these questions with only a single answer in some cases. The best strategy is to read all the answers and mark the correct ones. Use your note paper to keep track if it's confusing.

# ## Sample Choose All That Apply Question

Which of the following commands creates a second file that is identical to the first? (Choose all that apply.)

+   - A. cp file1 file2
+   - B. cat file1 ; file2
+   - C. cp < file1 > file2
+   - D. dd if=file1 of=file2
+   - E. cat file1 > file2

Answers A, D, and E are correct. Using the cp command to copy one file to the other is normal, the difference between answers B and E is the incorrect use of the ; symbol to another file. It must be followed by a program, and the unusual usage of the dd command will work in this case. Answer B is incorrect because files may not be redirected via a pipe symbol (|). Answer C is incorrect because the use of the < and > characters produces a syntax error.