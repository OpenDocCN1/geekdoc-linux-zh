

851 #define putname(name) free_page((unsigned long)(name))

853 enum (BDEV_FILE, BDEV_SWAP, BDEV_FS, BDEV_RAW);
854 extern void kill_fasync(struct fasync_struct *, int, int);
855 extern int register_blkdev(unsigned int, const char *,
            struct block_device_operations *);
856 extern int unregister_blkdev(unsigned int, const char *);
857 extern struct block_device *bdget(dev_t);
858 extern void bdput(struct block_device *);
859 extern int blkdev_open(struct inode *, struct file *);
860 extern struct file_operations def_blk_fops;
861 extern struct file_operations def_fifo_fops;
862 extern int ioctl_by_bdev(struct block_device *, unsigned, unsigned long);
863 extern int blkdev_get(struct block_device *, mode_t, unsigned, int);
864 extern int blkdev_put(struct block_device *, int);

866 /* fs/devices.c */
867 extern const struct block_device_operations *get_blkfops(unsigned int);
868 extern struct file_operations *get_chrifops(unsigned int, unsigned int);
869 extern int register_chrdev(unsigned int, const char *, struct file_operations *);
870 extern int unregister_chrdev(unsigned int, const char *);
871 extern int chrdev_open(struct inode *, struct file *);
872 extern const char * bdename(kdev_t);
873 extern const char * cdename(kdev_t);
874 extern const char * kdevname(kdev_t);
875 extern void init_special_inode(struct inode *, umode_t, int);

877 /* Invalid inode operations -- fs/bad_inode.c */
878 extern void make_bad_inode(struct inode *);
879 extern int is_bad_inode(struct inode *);

881 extern struct file_operations connecting_fifo_fops;
882 extern struct file_operations read_fifo_fops;
883 extern struct file_operations write_fifo_fops;
884 extern struct file_operations read_pipe_fops;
885 extern struct file_operations write_pipe_fops;
886 extern struct file_operations rdwr_pipe_fops;

888 extern int fs_may_remount_ro(struct super_block *);
889 extern int fs_may_mount(kdev_t);

891 extern int try_to_free_buffers(struct page *);
892 extern void refile_buffer(struct buffer_head * buf);

894 #define BUF_CLEAN       0
895 #define BUF_LOCKED      1 /* Buffers scheduled for write */
896 #define BUF_DIRTY       2 /* Dirty buffers, not yet scheduled for write */
897 #define BUF_PROTECTED   3 /* Ramdisk persistent storage */
898 #define NR_LIST         4

900 /*
901 * This is called by bh->b_end_io() handlers when I/O has completed.
902 */

904 extern inline void mark_buffer_uptodate(struct buffer_head * bh, int on)
905 {
906 	if (on)
907 		set_bit(BH_Uptodate, &bh->b_state);
908 	else
909 		clear_bit(BH_Uptodate, &bh->b_state);
910 }
911
912 #define atomic_set_buffer_clean(bh) test_and_clear_bit(BH_Dirty, &(bh)->b_state)
913
914 extern inline void __mark_buffer_clean(struct buffer_head *bh)
915 {
916 	refile_buffer(bh);
917 }
918
919 extern inline void mark_buffer_clean(struct buffer_head * bh)
920 {
921 	if (atomic_set_buffer_clean(bh))
922 		__mark_buffer_clean(bh);
923 }
924
925 #define atomic_set_buffer_protected(bh) test_and_set_bit(BH_Protected,
926 	&(bh)->b_state)
927 extern inline void __mark_buffer_protected(struct buffer_head *bh)
928 {
929 	refile_buffer(bh);
930 }
931
932 extern inline void mark_buffer_protected(struct buffer_head * bh)
933 {
934 	if (!atomic_set_buffer_protected(bh))
935 		__mark_buffer_protected(bh);
936 }
937
938 extern void FASTCALL(__mark_buffer_dirty(struct buffer_head *bh, int flag));
939 extern void FASTCALL(mark_buffer_dirty(struct buffer_head *bh, int flag));
940
941 #define atomic_set_buffer_dirty(bh) test_and_set_bit(BH_Dirty, &(bh)->b_state)
942
943 extern void balance_dirty(kdev_t);
944 extern int check_disk_change(kdev_t);
945 extern int invalidate_inodes(struct super_block *);
946 extern void invalidate_inode_pages(struct inode *);
947 #define invalidate_buffers(dev) __invalidate_buffers((dev), 0)
948 #define destroy_buffers(dev) __invalidate_buffers((dev), 1)
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
963
964 extern int open_namei(const char *, int, int, struct nameidata *);
965
966 extern int kernel_read(struct file *, unsigned long, char *, unsigned long);
967 extern struct file * open_exec(const char *);
968
969 /* fs/dcache.c -- generic fs support functions */
970 extern int is_subdir(struct dentry *, struct dentry *);
971 extern ino_t find_inode_number(struct dentry *, struct qstr *);
972
973 /*
974 * Kernel pointers have redundant information, so we can use a
975 * scheme where we can return either an error code or a dentry
976 * pointer with the same return value.
977 *
978 * This should be a per-architecture thing, to allow different
979 * error and pointer decisions.
980 */
981 #define ERR_PTR(err)  ((void *)((long)(err)))
982 #define PTR_ERR(ptr)  ((long)(ptr))
983 #define IS_ERR(ptr)   ((unsigned long)(ptr) > (unsigned long)(-1000))
984
985 /*
986 * The bitmask for a lookup event:
987 * - follow links at the end
988 * - require a directory
989 * - ending slashes ok even for nonexistent files
990 * - internal "there are more path components" flag
991 */
992 #define LOOKUP_FOLLOW   (1)
993 #define LOOKUP_DIRECTORY (2)
994 #define LOOKUP_SLASHOK  (4)
995 #define LOOKUP_CONTINUE (8)
996 #define LOOKUP_POSITIVE (16)
997 #define LOOKUP_PARENT   (32)
998
999 /*
1000 * "descriptor" for what we're up to with a read for sendfile().
1001 * This allows us to use the same read code yet
1002 * have multiple different users of the data that
1003 * we read from a file.
1004 *
1005 * The simplest case just copies the data to user
1006 * mode.
1007 */
1008 typedef struct {
1009 	size_t written;
1010 	size_t count;
1011           char * buf;
1012           int error;
1013 } read_descriptor_t;
1014
1015 typedef int (*read_actor_t)(read_descriptor_t *, struct page *, unsigned long,
1016 unsigned long);
1017
1018 extern struct dentry * lookup_dentry(const char *, unsigned int);
1019 extern int walk_init(const char *, unsigned, struct nameidata *);
1020 extern int walk_name(const char *, unsigned, struct nameidata *);
1021 extern struct dentry * lookup_one(const char *, struct dentry *);
1022 extern struct dentry * __namei(const char *, unsigned int);
1023
1024 #define namei(pathname)                 __namei(pathname, LOOKUP_FOLLOW)
1025 #define lnamei(pathname)                __namei(pathname, 0)
1026
1027 extern void iput(struct inode *);
1028 extern struct inode * igrab(struct inode *);
1029 extern ino_t iunique(struct super_block *, ino_t);
1030
1031 typedef int (*find_inode_t)(struct inode *, unsigned long, void *);
1032 extern struct inode * iget4(struct super_block *, unsigned long, find_inode_t,
1033 void *);
1034 static inline struct inode *iget(struct super_block *sb, unsigned long ino)
1035 {
1036         return iget4(sb, ino, NULL, NULL);
1037 }
1038
1039 extern void clear_inode(struct inode *);
1040 extern struct inode * get_empty_inode(void);
1041
1042 extern void insert_inode_hash(struct inode *);
1043 extern void remove_inode_hash(struct inode *);
1044 extern struct file * get_empty_filp(void);
1045 extern void file_move(struct file *f, struct list_head *list);
1046 extern void file_move_to(struct file *new, struct file *old);
1047 extern struct buffer_head * get_hash_table(kdev_t, int, int);
1048 extern struct buffer_head * getblk(kdev_t, int, int);
1049 extern int ll_rw_block(int, int, struct buffer_head * bh[]);
1050 extern int is_read_only(kdev_t);
1051 extern void __brelse(struct buffer_head *);
1052 extern inline void brelse(struct buffer_head *buf)
1053 {
1054         if (buf)
1055                 __brelse(buf);
1056 }
1057
1058 extern void __bforget(struct buffer_head *);
1059 extern inline void bforget(struct buffer_head *buf)
1060 {
1061         if (buf)
1062                 __bforget(buf);
1063 }
1064
1065 extern void set_blocksize(kdev_t, int);
1066 extern unsigned int get_hardblocksize(kdev_t);

