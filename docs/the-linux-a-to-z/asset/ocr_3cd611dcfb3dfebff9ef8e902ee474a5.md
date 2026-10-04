![](bbox=[0.08, 0.1, 0.9, 0.28])

Figure 31.8 Layout of an ext2 block group.

it worth doing a read ahead of several blocks at the same time into the buffer cache, while the disk heads are in the right place, so that the data will already be in the cache when it is required.

There are many other facilities provided by the ext2 filesystem which make it the best current choice as a general purpose Linux filesystem. It also has the flexibility for much future expansion, and development is continuously in progress.