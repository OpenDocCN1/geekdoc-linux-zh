
# Header Definitions

## Function Declarations

```
949 extern void __invalidate_buffers(kdev_t dev, int);
950 extern int floppy_is_wp(int);
951 extern void sync_inodes(kdev_t);
952 extern void write_inode_now(struct inode *);
953 extern void sync_dev(kdev_t);
954 extern int fsync_dev(kdev_t);
955 extern void sync_supers(kdev_t);
956 extern int bmap(struct inode *, int);
957 extern int notify_change(struct dentry *, struct iattr *);
958 extern int permission(struct inode *, int);
959 extern int get_write_access(struct inode *);
960 extern void put_write_access(struct inode *);
961 extern struct dentry * do_mknod(const char *, int, dev_t);
962 extern int do_pipe(int *);
964 extern int open_namei(const char *, int, int, struct nameidata *);
966 extern int kernel_read(struct file *, unsigned long, char *, unsigned long);
967 extern struct file * open_exec(const char *);
```

## Filesystem Support

/* fs/dcache.c -- generic fs support functions */
```
970 extern int is_subdir(struct dentry *, struct dentry *);
971 extern ino_t find_inode_number(struct dentry *, struct qstr *);
```

## Error Handling Macros

/*
 * Kernel pointers have redundant information, so we can use a
 * scheme where we can return either an error code or a dentry
 * pointer with the same return value.
 *
 * This should be a per-architecture thing, to allow different
 * error and pointer decisions.
 */

```
981 #define ERR_PTR(err)  ((void *)((long)(err)))
982 #define PTR_ERR(ptr)  ((long)(ptr))
983 #define IS_ERR(ptr)   ((unsigned long)(ptr) > (unsigned long)(-1000))
```

## Lookup Event Bitmask

/*
 * The bitmask for a lookup event:
 * - follow links at the end
 * - require a directory
 * - ending slashes ok even for nonexistent files
 * - internal "there are more path components" flag
 */

```
992 #define LOOKUP_FOLLOW   (1)
993 #define LOOKUP_DIRECTORY (2)
994 #define LOOKUP_SLASHOK  (4)
995 #define LOOKUP_CONTINUE (8)
996 #define LOOKUP_POSITIVE (16)
997 #define LOOKUP_PARENT   (32)
```

## Read Descriptor

/*
 * "descriptor" for what we're up to with a read for sendfile().
 * This allows us to use the same read code yet
 * have multiple different users of the data that
 * we read from a file.
 *
 * The simplest case just copies the data to user
 * mode.
 */

```
1008 typedef struct {
1009 	size_t written;
1010 	size_t count;
1011           char * buf;
1012           int error;
1013 } read_descriptor_t;

1015 typedef int (*read_actor_t)(read_descriptor_t *, struct page *, unsigned long,
1016 unsigned long);
```

## Path and Inode Functions

```
1018 extern struct dentry * lookup_dentry(const char *, unsigned int);
1019 extern int walk_init(const char *, unsigned, struct nameidata *);
1020 extern int walk_name(const char *, unsigned, struct nameidata *);
1021 extern struct dentry * lookup_one(const char *, struct dentry *);
1022 extern struct dentry * __namei(const char *, unsigned int);

1024 #define namei(pathname)                 __namei(pathname, LOOKUP_FOLLOW)
1025 #define lnamei(pathname)                __namei(pathname, 0)

1027 extern void iput(struct inode *);
1028 extern struct inode * igrab(struct inode *);
1029 extern ino_t iunique(struct super_block *, ino_t);

1031 typedef int (*find_inode_t)(struct inode *, unsigned long, void *);
1032 extern struct inode * iget4(struct super_block *, unsigned long, find_inode_t,
1033 void *);
1034 static inline struct inode *iget(struct super_block *sb, unsigned long ino)
1035 {
1036         return iget4(sb, ino, NULL, NULL);
1037 }

1039 extern void clear_inode(struct inode *);
1040 extern struct inode * get_empty_inode(void);

1042 extern void insert_inode_hash(struct inode *);
1043 extern void remove_inode_hash(struct inode *);
1044 extern struct file * get_empty_filp(void);
1045 extern void file_move(struct file *f, struct list_head *list);
1046 extern void file_move_to(struct file *new, struct file *old);
1047 extern struct buffer_head * get_hash_table(kdev_t, int, int);
```
