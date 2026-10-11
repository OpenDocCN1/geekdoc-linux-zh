+   * `key_cache_age_threshold` indicates how long buffers stay unused in the hot sub-chain of the key cache before being moved to the warm sub-chain. Higher values enable blocks to remain in the hot sub-chain longer.The default is 300. The minimum value is 100.

One key cache is the default and has a name of default. If you refer to a key cache component variable without using a cache name, MySQL uses the default cache.Thus, key_buffer_size and default.key_buffer_size refer to the same variable. Key cache names must be legal identifiers and are not case sensitive.They can be quoted like any other identifier (see Section 2.2, “MySQL Identifier Syntax and Naming Rules”).

To create a new key cache, simply assign a value to one of the components of the associated variable. For example, to create a cache named my_cache with a size of 24MB, at server startup, add these lines to the server option file:

```
[mysqld]
my_cache.key_buffer_size = 24M
```

To create the cache at runtime, use this statement:

```
SET GLOBAL my_cache.key_buffer_size = 24*1024*1024;
```

The GLOBAL keyword is necessary because key caches are global. No special privileges are required to access component values, but you must have the SUPER privilege to set them.

After you create a key cache, you can assign MyISAM tables to it with CACHE INDEX. This statement names a key cache and one or more tables to be assigned to it.The following statement assigns the member and president tables from the samplib database to the cache named my_cache:

```
CACHE INDEX member, president IN my_cache;
```

You can also preload table indexes into their assigned cache with LOAD INDEX INTO CACHE if you choose:

```
LOAD INDEX INTO CACHE member, president;
```

It is not necessary to preload the indexes, but the server reads index blocks sequentially if you do.This is more efficient than waiting for them to be fetched as needed.

The CACHE INDEX and LOAD INDEX INTO CACHE statements require that you have the INDEX privilege for the tables that are to be assigned to or preloaded into a cache.

To destroy a key cache, set its size to zero.Any tables assigned to the cache are reassigned to the default cache. If you set the size of the default key cache to zero, indexes of tables assigned to it are processed using filesystem caching the same way as for MyISAM data files.

Key cache assignments last only until the server shuts down.To make assignments each time the server starts, place the appropriate CACHE INDEX and LOAD INDEX INTO CACHE statements in a file and start the server with an --init-file option that names the file.