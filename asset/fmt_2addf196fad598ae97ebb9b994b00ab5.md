
```c
extern struct buffer_head * getblk(kdev_t, int, int);

extern int ll_rw_block(int, int, struct buffer_head * bh[]);

extern int is_read_only(kdev_t);

extern void __brelse(struct buffer_head *);

extern inline void brelse(struct buffer_head *buf)
{
    if (buf)
        __brelse(buf);
}

extern void __bforget(struct buffer_head *);

extern inline void bforget(struct buffer_head *buf)
{
    if (buf)
        __bforget(buf);
}

extern void set_blocksize(kdev_t, int);
extern unsigned int get_hardblocksize(kdev_t);
```

## 文件系统
