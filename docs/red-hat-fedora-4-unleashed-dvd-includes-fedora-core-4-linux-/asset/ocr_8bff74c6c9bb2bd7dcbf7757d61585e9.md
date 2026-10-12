An 8MB query cache should be enough for most people, but larger sites might want 16MB or even 32MB if you are storing a particularly large amount of data. Very few sites will have need to go beyond a 32MB query cache, but keep an eye on the Qcache_lowmem_prunes value to ensure you have enough RAM allocated.

Using the query cache does not incur much of a performance hit. When MySQL calculates the result of a query normally, it simply throws it away when the connection closes. With the query cache, it skips the throwing away, and so there is no extra work being done. If your site does have many updates and deletes, be sure to check whether you get any speed boost at all from the query cache.

# Miscellaneous Tweaks

If you have tuned your key buffer and optimized your query cache and yet still find your site struggling, there are a handful more smaller changes you make that will add some more speed.

When reading from tables, MySQL has to open the file that stores the table data. How many files it keeps open at a time is defined by the table_cache setting, which is set to 64 by default. You can increase this setting if you have more than 64 tables, but you should be aware that Fedora does impose limits on MySQL about how many files it can have open at a time. Going beyond 256 is not recommended unless you have a particularly DB-heavy site and know exactly what you are doing.

The other thing you can tweak is the size of the read buffer, which is controlled by read_buffer_size and read_buffer_rnd_size. Both of these are allocated per connection, which means you should be very careful to have large numbers. Whatever you choose, read_buffer_rnd_size should be three to four times the size of read_buffer_size, so if read_buffer_size is 1MB (suitable for very large databases), read_buffer_rnd_size should be 4MB.

# Query Optimization

The biggest speed-ups can be seen by reprogramming your SQL statements so they are more efficient. If you follow these tips, your server will thank you:

+   - Select as little data as possible. Rather than SELECT *, select only the fields you need.
+   - If you only need a few fields, use LIMIT to select the number you need.
+   - Declare fields as NOT NULL when creating tables to save space and increase speed.
+   - Provide default values for fields, and use them where you can.
+   - Be very careful with table joins because they are the easiest way to write inefficient queries.
+   - If you must use joins, be sure you join on fields that are indexed.