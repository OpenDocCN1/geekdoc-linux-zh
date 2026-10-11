![](bbox=[0.27, 0.11, 0.76, 0.48])

# I/O vectors

The bi_io_vec field points to an array of bio_vec structures. These structures are used as lists of individual segments in this specific block I/O operation. Each bio_vec is treated as a vector of the form <page, offset, len>, which describes a specific segment: the physical page on which it lies, the location of the block as an offset into the page, and the length of the block starting from the given offset. The full array of these vectors describes the entire buffer. The bio_vec structure is defined in <linux/bio.h>:

```
```c
struct bio_vec {
    /* pointer to the physical page on which this buffer resides */
    struct page *bv_page;
    /* the length in bytes of this buffer */
    unsigned int bv_len;
    /* the byte offset within the page where the buffer resides */
    unsigned int bv_offset;
};
```
```

In each given block I/O operation, there are bi_vcnt vectors in the bio_vec array starting with bi_io_vec. As the block I/O operation is carried out, the bi_idx field is used to point to the current index into the array.

In summary, each block I/O request is represented by a bio structure. Each request is composed of one or more blocks, which are stored in an array of bio_vec structures.