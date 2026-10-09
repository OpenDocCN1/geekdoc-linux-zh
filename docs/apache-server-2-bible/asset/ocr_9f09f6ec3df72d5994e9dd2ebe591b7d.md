symbolic matches the server's own. For example, the following configuration in the main server section (that is, outside any virtual host configuration) of `httpd.conf` will instruct Apache not to follow symbolic links, effectively disabling all symbolic link access via Web.

```
<Directory />
    Options -FollowSymLinks
</Directory>
```

Unfortunately, this comes with a significant performance price. For each request, Apache performs an additional system call, `lstat()`, to ensure that it is not violating your don't-follow-symbolic-link policy.

To increase performance while having symbolic links and good security, do the following:

+   1. Find a way not to use any symbolic links on your Web document tree. You can use the `find your_top_web_directory -type l -print` command to find all the existing symbolic links in your top Web directory; then you can figure out how to avoid them.

+   2. Use the following configuration in the main server section of `httpd.conf` to enable symbolic links:

```
<Directory />
    Options FollowSymLinks
</Directory>
```

+   3. If you must disable symbolic links, consider narrowing the directory scope with a specific directory name. For example, if you want to disallow symbolic links in a directory called `my_dir` but allow symbolic links everywhere else (for performance), you can use this configuration:

```
<Directory />
    Options FollowSymLinks
</Directory>

<Directory /my_dir>
    Options -FollowSymLinks
</Directory>
```

+   4. Similarly, you can use the `SymlinksIfOwnerMatch`:

```
<Directory />
    Options FollowSymLinks
</Directory>

<Directory /my_dir>
    Options -FollowSymLinks +SymlinksIfOwnerMatch
</Directory>
```

Here Apache will follow symbolic links in the `/my_dir` directory if their owner ID matches the server's user ID.