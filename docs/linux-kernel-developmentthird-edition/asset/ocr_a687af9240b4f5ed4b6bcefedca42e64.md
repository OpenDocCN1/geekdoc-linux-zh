In another example of horrible kernel naming, use `kfifo_len()` to obtain the number of bytes enqueued in a kfifo:

```
```
static inline unsigned int kfifo_len(struct kfifo *fifo);
```
```

To find out the number of bytes available to write into a kfifo, call `kfifo_avail()`:

```
```
static inline unsigned int kfifo_avail(struct kfifo *fifo);
```
```

Finally, `kfifo_is_empty()` and `kfifo_is_full()` return nonzero if the given kfifo is empty or full, respectively, and zero if not:

```
```
static inline int kfifo_is_empty(struct kfifo *fifo);
static inline int kfifo_is_full(struct kfifo *fifo);
```
```

# Resetting and Destroying the Queue

To reset a kfifo, jetisonning all the contents of the queue, call `kfifo_reset()`:

```
```
static inline void kfifo_reset(struct kfifo *fifo);
```
```

To destroy a kfifo allocated with `kfifo_alloc()`, call `kfifo_free()`:

```
```
void kfifo_free(struct kfifo *fifo);
```
```

If you created your kfifo with `kfifo_init()`, it is your responsibility to free the associated buffer. How you do so depends on how you created it. See Chapter 12 for a discussion on allocating and freeing dynamic memory.

# Example Queue Usage

With these interfaces under our belt, let’s take a look at a simple example of using a kfifo. Assume we created a kfifo pointed at by `fifo` with a queue size of 8KB. We can now enqueue data onto the queue. In this example, we enqueue simple integers. In your own code, you will likely enqueue more complicated, task-specific structures. Using integers in this example, let’s see exactly how the kfifo works:

```
```
unsigned int i;

/* enqueue [0, 32) to the kfifo named "fifo" */
for (i = 0; i < 32; i++)
	kfifo_in(fifo, &i, sizeof(i));
```
```

The kfifo named `fifo` now contains 0 through 31, inclusive. We can take a peek at the first item in the queue and verify it is 0:

```
```
unsigned int val;
int ret;

ret = kfifo_out_peek(fifo, &val, sizeof(val), 0);
if (ret != sizeof(val))
	return -EINVAL;
```
```