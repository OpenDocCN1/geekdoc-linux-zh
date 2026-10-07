# # Linux Swap Space Partition

How big should the swap space partition be? There’s no single size that works for all installations, unfortunately. Generally, since the swap space is used as an extension of physical RAM, the more RAM you have, the less swap space is required. You can add the amount of swap space and the amount of RAM together to get the amount of RAM Linux will use. For example, if you have 8MB of RAM on your machine’s motherboard and a 16MB swap space partition, Linux will behave as though you had 24MB RAM total.

Linux uses the swap space by moving pages of physical RAM to the swap space when it doesn’t need that page at the moment, and vice versa when it needs the memory page. So why not make a very large swap space and let Linux think it’s in heaven? Because the swap space is much slower in access time than RAM, and there is a point where the size of the swap space acts against your Linux system’s efficiency, instead of for it.

Swap space may not even be needed if you have lots of RAM. For example, if you have 16MB of physical RAM and don’t intend to do any application development or run X, you won’t make much use of the swap space because Linux can fit everything it needs in the 16MB. (You still should have a small swap space, just in case.)

If you are running X, developing applications, or running memory-hog applications, such as databases, swap space is crucial even if you have lots of physical RAM. Even 16MB RAM is not enough for X, so you need swap space.

A good rule is to create a swap space with the maximum size limit of 16MB. Unless you have a very small-capacity hard disk, this won’t be a major drain on your resources, and it gives Linux plenty to work with. If you don’t want to allocate this much swap space, a good rule is to have a total of 16MB RAM (swap space plus physical RAM). Don’t eliminate the swap space completely, though, unless you have a lot of RAM. At a minimum, set up a 4MB swap space. Running out of RAM can cause Linux to lock up or crash, which isn’t a pretty sight!

# # Setting Up Partitions

Because the versions of `fdisk` in DOS, OS/2, UNIX, and Linux all differ, we won’t bother explaining all the steps. The `fdisk` utility is very easy to use, so if you have used PC machines for a while, this will not be a problem for you. Remember that `fdisk` destroys existing data on your disk! You can set up your Linux disk partitions either from DOS or from within Linux. It really doesn’t matter which approach you use, although the DOS `fdisk` program is a little easier to use than Linux’s. If you are using DOS’s `fdisk` to repartition a DOS area on your drives, you might as well use it to set up the Linux swap space and filesystem partitions, too.