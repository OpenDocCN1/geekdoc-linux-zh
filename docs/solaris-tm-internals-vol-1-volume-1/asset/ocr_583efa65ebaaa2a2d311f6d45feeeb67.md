```
```c
extern struct mod_ops mod_fsops;
static struct modfs modfs = {
        &mod_fsops,
        "vnode_file pseudo file system",
        &vfw
};

static struct modlinkage modlinkage = {
        MODREV_1,
        &modfs,
        NULL
};

int
_init(void)
{
        int     error;

        mutex_init(&vnfslock, NULL, MUTEX_DEFAULT, NULL);
        rw_init(&vnfsnodes_lock, NULL, RW_DEFAULT, NULL);
        error = mod_install(&modlinkage);
        if (error) {
                mutex_destroy(&vnfslock);
                rw_destroy(&vnfsnodes_lock);
        }
        myfs_init_otherstuff();
        return (error);
}

int
_fini(void)
{
        int     error;

        vnfs_vnlist_destroy();
        error = mod_remove(&modlinkage);
        if (error) {
                return (error);
        }
        mutex_destroy(&vnfslock);
        rw_destroy(&vnfsnodes_lock);
        return (0);
}

int
_info(struct modinfo *modinfop)
{
        return (mod_info(&modlinkage, modinfop));
}

static struct vfsw vfw = {
        "myfs",
        myfsinit,
        &myfs_vfsops,
        0
};

static int
myfsinit(struct vfsw *vswp, int fstyp)
{
        vswp->vfsw_vfsops = &myfs_vfsops;
        myfstype = fstyp;
        (void) myfs_init();
        return (0);
}
```
```