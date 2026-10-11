
not have an explicit reason to move through the list in reverse, don't—just use `list_for_each_entry()`.

## Iterating While Removing

The standard list iteration methods are not appropriate if you are removing entries from the list as you iterate. The standard methods rely on the fact that the list entries are not changing out from under them, and thus if the current entry is removed in the body of the loop, the subsequent iteration cannot advance to the next (or previous) pointer. This is a common pattern in loops, and programmers solve it by storing the next (or previous) pointer in a temporary variable $prior$ to a potential removal operation. The Linux kernel provides a routine to handle this situation for you:

```
list_for_each_entry_safe(pos, next, head, member)
```

You use this version in the same manner as `list_for_each_entry()`, except that you provide the next pointer, which is of the same type as pos. The next pointer is used by the `list_for_each_entry_safe()` macro to store the next entry in the list, making it safe to remove the current entry. Let’s consider an example, again in inotify:

```
void inotify_inode_is_dead(struct inode *inode)
{
    struct inotify_watch *watch, *next;

    mutex_lock(&inode->inotify_mutex);
    list_for_each_entry_safe(watch, next, &inode->inotify_watches, i_list) { 
        struct inotify_handle *ih = watch->ih;
        mutex_lock(ih->mutex);
        inotify_remove_watched_locked(ih, watch); /* Deletes watch */
        mutex_unlock(ih->mutex);
    }
    mutex_unlock(&inode->inotify_mutex);
}
```

This function iterates over and removes all the entries in the $inotify\_watches$ list. If the standard `list_for_each_entry()` were used, this code would introduce a use-after-free bug, as moving to the next item in the list would require accessing watch, which was destroyed.

If you need to iterate over a linked list in reverse and potentially remove elements, the kernel provides `list_for_each_entry_safe_reverse()`:

```
list_for_each_entry_safe_reverse(pos, n, head, member)
```

Usage is the same as with `list_for_each_entry_safe()`.

## You May Still Need Locking!

The "safe" variants of `list_for_each_entry()` protect you only from removals from the list *within* the body of the loop. If there is a chance of concurrent removals from other code—or any other form of concurrent list manipulation—you need to properly lock access to the list.

See Chapters 9, "An Introduction to Kernel Synchronization," and Chapter 10, "Kernel Synchronization Methods," for a discussion on synchronization and locking.

## Other Linked List Methods

Linux provides myriad other list methods, enabling seemingly every conceivable way to access and manipulate a linked list. All these methods are defined in the header file `<linux/list.h>`.

## Queues

A common programming pattern in any operating system kernel is *producer* and *consumer*. In this pattern, a producer creates data—say, error messages to be read or networking packets to be processed—while a consumer, in turn, reads, processes, or otherwise *consumes* the data. Often the easiest way to implement this pattern is with a *queue*. The producer pushes data onto the queue and the consumer pulls data off the queue. The consumer retrieves the data in the order it was enqueued. That is, the first data on the queue is the first data off the queue. For this reason, queues are also called *FIFOs*, short for *first-in, first-out*. See Figure 6.5 for an example of a standard queue.

![](img/48bc90306f7476ca73ca7a99267ff690_122_0.png)

Figure 6.5 A queue (FIFO).

The Linux kernel's generic queue implementation is called **kfifo** and is implemented in `kernel/kfifo.c` and declared in `<linux/kfifo.h>`. This section discusses the API after an update in 2.6.33. Usage is slightly different in kernel versions prior to 2.6.33—double-check `<linux/kfifo.h>` before writing code.

### kfifo

Linux's **kfifo** works like most other queue abstractions, providing two primary operations: enqueue (unfortunately named *in*) and dequeue (*out*). The **kfifo** object maintains two offsets into the queue: an *in offset* and an *out offset*. The *in offset* is the location in the queue to which the next enqueue will occur. The *out offset* is the location in the queue from which the next dequeue will occur. The *out offset* is always less than or equal to the *in offset*. It wouldn't make sense for it to be greater; otherwise, you could dequeue data that had not yet been enqueued.

The enqueue (*in*) operation copies data into the queue, starting at the *in offset*. When complete, the *in offset* is incremented by the amount of data enqueued. The dequeue (*out*) operation copies data out of the queue, starting from the *out offset*. When complete, the *out offset* is incremented by the amount of data enqueued. When the *out offset* is equal to the *in offset*, the queue is empty: No more data can be dequeued until more data is enqueued. When the *in offset* is equal to the length of the queue, no more data can be enqueued until the queue is reset.

### Creating a Queue

To use a **kfifo**, you must first define and initialize it. As with most kernel objects, you can do this dynamically or statically. The most common method is dynamic:

```
int kfifo_alloc(struct kfifo *fifo, unsigned int size, gfp_t gfp_mask);
```

This function creates and initializes a **kfifo** with a queue of *size* bytes. The kernel uses the *gfp mask* *gfp_mask* to allocate the queue. (We discuss memory allocations in Chapter 12, “Memory Management”.) Upon success, `kfifo_alloc()` returns zero; on error it returns a negative error code. Following is a simple example:

```
struct kfifo fifo; int ret;

ret = kfifo_alloc(&fifo, PAGE_SIZE, GFP_KERNEL); if (ret)         return ret;

/* ‘fifo’ now represents a PAGE_SIZE-sized queue ... */
```

If you want to allocate the buffer yourself, you can:

```
void kfifo_init(struct kfifo *fifo, void *buffer, unsigned int size);
```

This function creates and initializes a kfifo that will use the *size* bytes of memory pointed at by *buffer* for its queue. With both kfifo_alloc() and kfifo_init(), *size* must be a power of two.

Statically declaring a kfifo is simpler, but less common:

```
DECLARE_KFIFO(name, size);
INIT_KFIFO(name);
```

This creates a static kfifo named name with a queue of *size* bytes. As before, *size* must be a power of 2.

### Enqueuing Data

When your kfifo is created and initialized, enqueuing data into the queue is performed via the kfifo_in() function:

```
unsigned int kfifo_in(struct kfifo *fifo, const void *from, unsigned int len);
```

This function copies the *len* bytes starting at *from* into the queue represented by *fifo*. On success it returns the number of bytes enqueued. If less than *len* bytes are free in the queue, the function copies only up to the amount of available bytes. Thus the return value can be less than *len* or even zero, if nothing was copied.

### Dequeuing Data

When you add data to a queue with kfifo_in(), you can remove it with kfifo_out():

```
unsigned int kfifo_out(struct kfifo *fifo, void *to, unsigned int len);
```

This function copies at most *len* bytes from the queue pointed at by *fifo* to the buffer pointed at by *to*. On success the function returns the number of bytes copied. If less than *len* bytes are in the queue, the function copies less than requested.

When dequeued, data is no longer accessible from the queue. This is the normal usage of a queue, but if you want to "peek" at data within the queue without removing it, you can use kfifo_out_peek():

```
unsigned int kfifo_out_peek(struct kfifo *fifo, void *to, unsigned int len, 
                            unsigned int offset);
```

This works the same as kfifo_out(), except that the *out* offset is not incremented, and thus the dequeued data is available to read on a subsequent call to kfifo_out(). The parameter *offset* specifies an index into the queue; specify zero to read from the head of the queue, as kfifo_out() does.

### Obtaining the Size of a Queue

To obtain the total size in bytes of the buffer used to store a kfifo's queue, call kfifo_size():

```
static inline unsigned int kfifo_size(struct kfifo *fifo);
```
