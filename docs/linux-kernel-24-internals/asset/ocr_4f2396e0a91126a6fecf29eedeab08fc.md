Linux supports up to 6 arguments for system calls. They are passed in %ebx, %ecx, %edx, %esi, %edi (and %ebp used temporarily, see _syscall6() in asm-i386/unistd.h). The system call number is passed via %eax.

# ## 2.12 Atomic Operations

There are two types of atomic operations: bitmaps and `atomic_t`. Bitmaps are very convenient for maintaining a concept of “allocated” or “free” units from some large collection where each unit is identified by some number, for example free inodes or free blocks. They are also widely used for simple locking, for example to provide exclusive access to open a device. An example of this can be found in `arch/i386/kernel/microcode.c`:

```
```
/*
 *  Bits in microcode_status. (31 bits of room for future expansion)
 */
#define MICROCODE_IS_OPEN    0       /* set if device is in use */

static unsigned long microcode_status;
```
```

There is no need to initialise `microcode_status` to 0 as BSS is zero–cleared under Linux explicitly.

```
```
/*
 * We enforce only one user at a time here with open/close.
 */
static int microcode_open(struct inode *inode, struct file *file)
{
    if (!capable(CAP_SYS_RAWIO))
        return -EPERM;

    /* one at a time, please */
    if (test_and_set_bit(MICROCODE_IS_OPEN, &microcode_status))
        return -EBUSY;

    MOD_INC_USE_COUNT;
    return 0;
}
```
```

The operations on bitmaps are:

+   * `void set_bit(int nr, volatile void *addr)`: set bit `nr` in the bitmap pointed to by `addr`.
+   * `void clear_bit(int nr, volatile void *addr)`: clear bit `nr` in the bitmap pointed to by `addr`.
+   * `void change_bit(int nr, volatile void *addr)`: toggle bit `nr` (if set clear, if clear set) in the bitmap pointed to by `addr`.
+   * `int test_and_set_bit(int nr, volatile void *addr)`: atomically set bit `nr` and return the old bit value.
+   * `int test_and_clear_bit(int nr, volatile void *addr)`: atomically clear bit `nr` and return the old bit value.
+   * `int test_and_change_bit(int nr, volatile void *addr)`: atomically toggle bit `nr` and return the old bit value.