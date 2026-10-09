+   -I <file> Read the contents of file as an input archive. This is used only with the -i option.

+   -v Verbose mode. Prints a list of file names.

+   -V Verbose mode, except it prints a dot (.) for each file read or written

The following are examples of combining the find and cpio commands:

To archive all the files from jsmith’s directory to an archive in /root called jsmith_backup.cpio, use the **find /home/jsmith/ | cpio -o > /root/jsmith_backup.cpio** command.

To restore the archive jsmith_backup.cpio in the /root directory to its original directory, use the **cpio -I < /root/jsmith_backup.cpio** command.

# Using dump and restore

The dump and restore programs are carryover programs from Unix. Administrators who are familiar with Unix use these programs because they are familiar and available; however, Linux is not a viable operating system for these older programs. The following is a comment from Linus Torvalds explaining why the use of dump is not advisable.

> **From:** Linus Torvalds <torvalds@transmeta.com>
**To:** Neil Conway <nconway.list@ukaea.org.uk>
**Subject:** Re: [PATCH] SMP race in ext2 - metadata corruption.
**Date:** Fri, 27 Apr 2001 09:59:46 -0700 (PDT)
**Cc:** Kernel Mailing List <linux-kernel@vger.kernel.org>

[ linux-kernel added back as a cc ]

On Fri, 27 Apr 2001, Neil Conway wrote:

> 

> I’m surprised that dump is deprecated (by you at least :)). What to

> use instead for backups on machines that can’t unmount disks regularly?

Note that dump simply won’t work reliably at all even in 2.4.x: the buffer cache and the page cache (where all the actual data is) are not coherent. This is only going to get even worse in 2.5.x, when the directories are moved into the page cache as well.

So anybody who depends on “dump” getting backups right is already playing russian roulette with their backups. It’s not at all guaranteed to get the right results—you may end up having stale data in the buffer cache that ends up being “backed up”.

Dump was a stupid program in the first place. Leave it behind.

> I’ve always thought “tar” was a bit undesirable (updates atimes or

> ctimes for example).

Right now, the cpio/tar/xxx solutions are definitely the best ones, and will work on multiple filesystems (another limitation of “dump”). Whatever problems they have, they are still better than the _guaranteed_(*) data corruptions of “dump”.

However, it may be that in the long run it would be advantageous to have a “filesystem maintenance interface” for doing things like backups and defragmentation.

Linus

(*) Dump may work fine for you a thousand times. But it _will_ fail under the right circumstances. And there is nothing you can do about it.

Given this problem, the use of dump and restore is strongly discouraged.