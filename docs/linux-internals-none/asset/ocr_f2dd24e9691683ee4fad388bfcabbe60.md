# ### Data Structures—include/linux/fsh

```
```
1  #ifndef _LINUX_FS_H
2  #define _LINUX_FS_H
3
4  /**
5   * This file has definitions for some important file table
6   * structures etc.
7   */
8
9  #include <linux/config.h>
10 #include <linux/linkage.h>
11 #include <linux/limits.h>
12 #include <linux/wait.h>
13 #include <linux/types.h>
14 #include <linux/vfs.h>
15 #include <linux/net.h>
16 #include <linux/kdev_t.h>
17 #include <linux/ioctl.h>
18 #include <linux/list.h>
19 #include <linux/dcache.h>
20 #include <linux/stat.h>
21 #include <linux/cache.h>
22 #include <linux/stddef.h>
23 #include <linux/string.h>
24
25 #include <asm/atomic.h>
26 #include <asm/bitops.h>
27
28 struct poll_table_struct;
29
30 /**
31  * It's silly to have NR_OPEN bigger than NR_FILE, but you can change
32  * the file limit at runtime and only root can increase the per-process
33  * nr_file rlimit, so it's safe to set up a ridiculously high absolute
34  * upper limit on files-per-process.
35  *
36  * Some programs (notably those using select()) may have to be
37  * recompiled to take full advantage of the new limits..
38  */
39
40 /** Fixed constants first: */
41 #undef NR_OPEN
42 #define NR_OPEN (1024*1024) /* Absolute upper limit on fd num */
43 #define INR_OPEN 1024       /* Initial setting for nrfile rlimits */
44
45 #define BLOCK_SIZE_BITS 10
46 #define BLOCK_SIZE (1<<BLOCK_SIZE_BITS)
47
48 /* And dynamically-tunable limits and defaults: */
49 extern int max_files, nr_files, nr_free_files;
50 extern int max_super_blocks, nr_super_blocks;
```
```