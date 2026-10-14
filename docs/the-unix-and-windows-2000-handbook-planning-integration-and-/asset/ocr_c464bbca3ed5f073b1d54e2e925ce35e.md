cially useful feature for the system administrator when preforming maintenance and upgrading software. The second entry in the `auto_master` defines the mount parameters for `/home`. When attempting to mount directories under `/home`, the automounter is directed to use the `auto_home` map, which is shown here.

```
```
#
#/etc/auto_home
#
local       -bg    earth:/usr/local
*           -bg    saturn:/home/users/&
```
```

By directing automountd to `auto_home`, we can customize how the automounter should act for the `/home` directory. In the example, `/etc/auto_home`, the first entry, directs automountd to mount `/home/local` from `earth:/usr/local` while running in the background. The second entry uses wildcard entries `*` and `&`. The `*` tells the automounter what to do with requests that are not explicitly defined in the map. The `&` is an expansion wildcard that expands the current request into the mount definition. For example, if user `ralph` attempts to mount `ralph`'s home directory using the command:

```
```
mars# cd /home/ralph
```
```

The automounter looks in the `auto_home` map and sees that `ralph` is not explicitly defined. All undefined requests are expanded using the `saturn:/home/users/&` entry. By replacing the `&` with `ralph`, `mars` will attempt to mount the filesystem `/home/users/ralph` from the system `saturn`.

If `/home/users/ralph` exists and is shared, it will be mounted; otherwise, `ralph` will see a “directory not found” error. As long as the filesystem has activity, it will remain mounted. After some period of time (the default time is generally five minutes), the automounter will attempt to unmount the filesystem as long as there is no activity.

No user intervention is necessary, and better yet, no root user intervention is needed. By releasing the NFS file-system, there is less chance for an NFS problem. You also reduce the resources necessary to manage NFS on the client system.

# Am-utils: 4.4BSD Automounter Utilities

The Am-utils comprise a suite of automounter tools that can be used in place of Sun’s automounter. The suite includes `amd`, the automounter daemon, and `amq`, the automounter query tool. Am-utils have been ported to AIX, HP-UX, Linux, and Solaris. They are available in source or binary form for each platform. The source provides configuration tools that greatly sim-