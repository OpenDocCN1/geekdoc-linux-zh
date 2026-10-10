+   3. \(show()\), which interprets the iterator passed to it and generates output strings to be displayed when a user reads the corresponding procs file. This method makes use of helpers such as \(seq\_printf()\), \(seq\_putc()\), and \(seq\_puts()\) to format the output.

+   4. \(stop()\), which is called at the end for cleanup.

The seq file interface automatically invokes these iterator methods to produce output in response to user operations on related procs files. You no longer need to worry about page-sized buffers and signaling the end of data.

Let's rewrite Listing C.2 making use of seq files. This is done in Listing C.3 by viewing the linked list as a sequence of nodes. The basic iterator object is the node, and each invocation of the \(next()\) method returns the next node in the list.

# Listing C.3. Using Seq Files to Simplify Listing C.2

```
Code View:
\#include <linux/seq_file.h>

/* start() method */
static void *
mydrv_seq_start(struct seq_file *seq, loff_t *pos)
{
 struct _mydrv_struct *p;
 loff_t off = 0;

 /* The iterator at the requested offset */
 list_for_each_entry(p, &mydrv_list, list) {
  if (*pos == off++) return p;
 }
 return NULL;
}

/* next() method */
static void *
mydrv_seq_next(struct seq_file *seq, void *v, loff_t *pos)
{
 /* 'v' is a pointer to the iterator returned by start() or
  by the previous invocation of next() */
 struct list_head *n = ((struct _mydrv_struct *)v)->list.next;

 ++*pos; /* Advance position */
 /* Return the next iterator, which is the next node in the list */
 return(n != &mydrv_list) ?
  list_entry(n, struct _mydrv_struct, list) : NULL;
}

/* show() method */
static int
mydrv_seq_show(struct seq_file *seq, void *v)
{
 const struct _mydrv_struct *p = v;

 /* Interpret the iterator, 'v' */
 seq_printf(seq, p->info);

```