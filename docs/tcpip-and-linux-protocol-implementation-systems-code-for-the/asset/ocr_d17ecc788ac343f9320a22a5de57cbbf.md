# TCP/IP and Linux Protocol Implementation

```
* Buffers may only be allocated from interrupts using a @gfp_mask of
* XGFP_ATOMIC;
*/
```

The code to allocate a socket buffer calls lower-level kernel functions to actually allocate the right type of memory.

# 5.128 Allocate socket buffer: linux/net/core/skbuff.c.

```
struct sk_buff *alloc_skb(unsigned int size, int gfp_mask)
{
    struct sk_buff *skb;
    u8 *data;

    if (in_interrupt() && (gfp_mask & __GFP_WAIT)) {
        static int count = 0;
        if (++count < 5) {
            printk(KERN_ERR "alloc_skb called nonatomically\n"
                   "  from interrupt %p\n", ___CALLER(size));
            BUG();();
        }
    }
    gfp_mask &= __GFP_WAIT;

    /* Get the HEAD */
    skb = skb_head_from_pool();
    if (skb == NULL) {
        skb = kmem_cache_alloc(skbuff_head_cache, cache, gfp_mask);
        if (skb == NULL)
            goto nodata;
    }

    /* Get the Data. Size must match skb_add_mtu().*/
    size = (size + 15) & ~15;
    data = kmalloc(size + sizeof(atomic_t), gfp_mask);
    if (data == NULL)
        goto nodata;

    /* XXX: does not include slab overhead */
    skb->truesize = size + sizeof(struct sk_buff);

    /* Load the data pointers. */
    skb->head = data;
    skb->tail = data;
    skb->end = data + size;

    /* Set up other state */
```