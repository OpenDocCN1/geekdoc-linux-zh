*write*: a file that’s 50 percent the old version, 50 percent the new version, and probably 100 percent unusable.

ZFS never overwrites the existing blocks in a file. When a file changes, ZFS identifies the blocks that must change and writes them to a new chunk of disk space. The old version is left intact. This is called copy-on-write (COW). With copy-on-write, a short write might lose the newest changes to the file, but the previous version of the file will remain intact.

Never corrupting files is a great benefit to copy-on-write, but COW opens up other possibilities. The metadata blocks are also copy-on-write, all the way up to the *uberblocks* that form the root of the ZFS pool’s data tree. ZFS creates snapshots by tracking the blocks that contain old versions of a file. While that sounds simple, the details are what will lead you astray.

# ## Snapshots

A snapshot is a copy of a dataset as it existed at a specific instant. Snapshots are read-only and never change. You can access the contents of a snapshot to access older versions of files or even deleted files. While snapshots are read-only, you can roll the dataset back to the snapshot. Take a snapshot before upgrading a system, and if the upgrade goes horribly wrong, you can fall back to the snapshot. ZFS uses snapshots to provide many features, such as boot environments (see “Boot Environments” on page 276). Best of all, depending on your data, snapshots can take up only tiny amounts of space.

Every dataset has a bunch of metadata, all built as a tree from a top-level block. When you create a snapshot, ZFS duplicates that top-level block. One of those metadata blocks goes with the dataset, while the other goes with the snapshot. The dataset and the snapshot share the data blocks within the dataset.

Deleting, modifying, or overwriting a file on the live dataset means allocating new blocks for the new data and disconnecting blocks containing the old data. Snapshots need some of those old data blocks,