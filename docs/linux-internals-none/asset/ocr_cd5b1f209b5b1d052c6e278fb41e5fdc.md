```
```
695 	ssize_t (*write) (struct file *, const char *, size_t, loff_t *);
696 	int (*readdir) (struct file *, void *, filldir_t);
697 	unsigned int (*poll) (struct file *, struct poll_table_struct *);
698 	int (*ioctl) (struct inode *, struct file *, unsigned int, unsigned
		long);
699 	int (*mmap) (struct file *, struct vm_area_struct *);
700 	int (*open) (struct inode *, struct file *);
701 	int (*flush) (struct file *);
702 	int (*release) (struct inode *, struct file *);
703 	int (*fsync) (struct file *, struct dentry *);
704 	int (*fasync) (int, struct file *, int);
705 	int (*lock) (struct file *, int, struct file_lock *);
706 	ssize_t (*readv) (struct file *, const struct iovec *, unsigned long,
		loff_t *);
707 	ssize_t (*writev) (struct file *, const struct iovec *, unsigned long,
		loff_t *);
708 };
709 
710 struct inode_operations {
711 	int (*create) (struct inode *,struct dentry *,int);
712 	struct dentry * (*lookup) (struct inode *,struct dentry *);
713 	int (*link) (struct dentry *,struct inode *,struct dentry *);
714 	int (*unlink) (struct inode *,struct dentry *);
715 	int (*symlink) (struct inode *,struct dentry *,const char *);
716 	int (*mkdir) (struct inode *,struct dentry *,int);
717 	int (*rmdir) (struct inode *,struct dentry *);
718 	int (*mknod) (struct inode *,struct dentry *,int,int);
719 	int (*rename) (struct inode *,struct dentry *,
		struct inode *, struct dentry *);
720 	int (*readlink) (struct dentry *, char *,int);
721 	int (*follow_link) (struct dentry *, struct nameidata *);
722 	void (*truncate) (struct inode *);
723 	int (*permission) (struct inode *, int);
724 	int (*revalidate) (struct dentry *);
725 	int (*setattr) (struct dentry *, struct iattr *);
726 	int (*getattr) (struct dentry *, struct iattr *);
727 };
728
729
730 /*
731 	* NOTE: write_inode, delete_inode, clear_inode, put_inode can be called
732 	* without the big kernel lock held in all filesystems.
733 	*/
734 struct super_operations {
735 	void (*read_inode) (struct inode *);
736 	void (*write_inode) (struct inode *);
737 	void (*put_inode) (struct inode *);
738 	void (*delete_inode) (struct inode *);
739 	void (*put_super) (struct super_block *);
740 	void (*write_super) (struct super_block *);
741 	int (*statfs) (struct super_block *, struct statfs *);
742 	int (*remount_fs) (struct super_block *, int *, char *);
743 	void (*clear_inode) (struct inode *);
744 	void (*umount_begin) (struct super_block *);
745 };
```
```