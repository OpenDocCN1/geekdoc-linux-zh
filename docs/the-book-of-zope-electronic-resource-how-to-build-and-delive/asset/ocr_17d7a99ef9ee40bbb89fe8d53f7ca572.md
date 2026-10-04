# 3.3.3.2 The Cache Parameters Tab

The Cache Parameters tab, shown in Figure 3-15, allows you to view and modify cache information, including the size and number of objects, as follows:

Total number of objects in the database

This field shows the total number of objects contained in the Zope database (in other words, stared in data.fs).

Total number of objects in all of the caches

This field shows the total number of objects currently in all caches.

Target size

This setting specifies the approximate maximum number of objects that can be contained in the cache at the same time. The smaller number, the smaller the cache. The default setting of 400 is generally sufficient. Using a smaller number will make Zope use less RAM, but at the expense of performance; a larger number could be used for high-traffic sites, with lots of objects, if your server has enough RAM.

Target maximum time between accesses

This setting specifies how much time must elapse between accesses an object will be automatically purged from the cache. The default setting of 60 means that objects that have not been accessed within the previous 60 minutes will be deleted from the cache.

| Database | Cache Parameters | Flush Cache |
|---|---|--|
| Database Management at /Control_Panel/Database | | Help |
| Total number of objects in the database | 5674 | |
| Total number of objects in all caches | 1133 | |
| Target Size | 400 | Change |
| Target max time between accesses | 60 | Change |

Figure 3-15: The Cache Parameters tab

# 3.3.3.3 The Flush Cache Tab

The Flush Cache tab, shown in Figure 3-16, lets you manually clear the contents of the cache, as follows:

Full Sweep

This option empties the cache. Specify the period of time during which an object must be accessed to prevent it being deleted from the cache; the default setting of 60 seconds means that all objects not accessed within the past 60 seconds will be deleted.

Minimize

This option removes more objects from the cache than Full Sweep and requires slightly longer to carry out.