```
2   * procfs4.c - create a "file" in /proc
3   * This program uses the seq_file library to manage the /proc file.
4   */
5
6   #include <linux/kernel.h> /* We are doing kernel work */
7   #include <linux/module.h> /* Specifically, a module */
8   #include <linux/proc_fs.h> /* Necessary because we use proc fs */
9   #include <linux/seq_file.h> /* for seq_file */
10  #include <linux/version.h>
11
12  #if LINUX_VERSION_CODE >= KERNEL_VERSION(5, 6, 0)
13  #define HAVE_PROC_OPS
14  #endif
15
16  #define PROC_NAME "iter"
17
18  /* This function is called at the beginning of a sequence.
19   * ie, when:
20   *   - the /proc file is read (first time)
21   *   - after the function stop (end of sequence)
22   */
23  static void *my_seq_start(struct seq_file *s, loff_t *pos)
24  {
25      static unsigned long counter = 0;
26
27      /* beginning a new sequence? */
28      if (*pos == 0) {
29          /* yes => return a non null value to begin the sequence */
30          return &counter;
31      }
32
33      /* no => it is the end of the sequence, return end to stop reading */
34      *pos = 0;
35      return NULL;
36  }
37
38  /* This function is called after the beginning of a sequence.
39   * It is called until the return is NULL (this ends the sequence).
40   */
41  static void *my_seq_next(struct seq_file *s, void *v, loff_t *pos)
42  {
43      unsigned long *tmp_v = (unsigned long *)v;
44      (*tmp_v)++;
45      (*pos)++;
46      return NULL;
47  }
48
49  /* This function is called at the end of a sequence. */
50  static void my_seq_stop(struct seq_file *s, void *v)
51  {
52      /* nothing to do, we use a static value in start() */
53  }
54
55  /* This function is called for each "step" of a sequence. */
56  static int my_seq_show(struct seq_file *s, void *v)
57  {
58      loff_t *pos = (loff_t *)v;
```