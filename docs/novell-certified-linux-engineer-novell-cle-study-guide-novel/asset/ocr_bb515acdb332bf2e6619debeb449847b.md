**FIGURE 5.32**
Implementing IRFs.

![](bbox=[0.26, 0.08, 0.91, 0.28])

For example, if you were to grant a different user object browse, create, and rename rights to the Finance container, he or she would have received those rights in spite of the IRF. IRFs only affect rights that are inherited from somewhere above in the tree hierarchy.

IRFs must be used with caution. Imagine what would happen if you were to block all the rights to the given container and there wasn't anyone else in the tree who had explicit assignment to the container: all access for everyone, including admin, would be cut off.

In the "old days" of NDS, the administrative tools in use at the time would allow you to do just that. Every now and then, you would hear horror stories about someone cutting off an entire branch of the eDirectory with an IRF, and he or she couldn't get it back.

Today, if you try to do this with a utility such as iManager, you will get a nasty warning indicating that if you implement the IRF, there's no one else in the tree who will be able to access the container.

You've just been given a crash course into the basics of eDirectory. As with Chapters 2 and 3, you've been given just enough to get you going.

Now, we're now going to change course and discuss two deeper eDirectory concepts: *partitioning* and *replication*.

# ## Managing eDirectory Partitioning and Replication

To understand eDirectory partitioning and replication, you must first realize that eDirectory is a distributed and replicated database. This is probably very different from other types of databases you have used in the past. It's definitely different from the way Linux and Windows NT user accounts are managed.