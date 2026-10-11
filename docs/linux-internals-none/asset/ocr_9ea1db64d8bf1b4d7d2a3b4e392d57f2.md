```
159 #define BLKSSZGET _IO(0x12, 104) /* get block device sector size */
160 #if 0
161 #define BLKPG _IO(0x12, 105) /* See blkpg.h */
162 #define BKELVGET _IO(0x12, 106) /* elevator get */
163 #define BKELVSET _IO(0x12, 107) /* elevator set */
164 /* This was here just to show that the number is taken -
165 probably all these _IO(0x12,*) ioctls should be moved to blkpg.h. */
166 #endif
167
168
169 #define BMAP_IOCT 1 /* obsolete - kept for compatibility */
170 #define FBMAP _IO(0x00,1) /* bmap access */
171 #define FGETBSZ _IO(0x00,2) /* get the block size used for bmap */
172
173 #ifdef _KERNEL_
174
175 #include <asm/semaphore.h>
176 #include <asm/byteorder.h>
177
178 extern void update_atime (struct inode *);
179 #define UPDATE_ATIME(inode) update_atime (inode)
180
181 extern void buffer_init(unsigned long);
182 extern void inode_init(void);
183 extern void file_table_init(void);
184 extern void dcache_init(void);
185
186 /* bh state bits */
187 #define BH_Uptodate 0 /* 1 if the buffer contains valid data */
188 #define BH_Dirty 1 /* 1 if the buffer is dirty */
189 #define BH_Lock 2 /* 1 if the buffer is locked */
190 #define BH_Req 3 /* 0 if the buffer has been invalidated */
191 #define BH_Mapped 4 /* 1 if the buffer has a disk mapping */
192 #define BH_New 5 /* 1 if the buffer is new and not yet written out */
193 #define BH_Protected 6 /* 1 if the buffer is protected */
194
195 /*
196 * Try to keep the most commonly used fields in single cache lines (16
197 * bytes) to improve performance. This ordering should be
198 * particularly beneficial on 32-bit processors.
199 *
200 * We use the first 16 bytes for data which is used in searches
201 * over the block hash lists (ie. getblk() and friends).
202 *
203 * The second 16 bytes we use for lru buffer scans, as used by
204 * sync_buffers() and refill_freelist(). -- sct
205 */
206 struct buffer_head {
207 /* First cache line: */
208 struct buffer_head *b_next; /* Hash queue list */
209 unsigned long b_blocknr; /* block number */
210 unsigned short b_size; /* block size */
211 unsigned short b_list; /* List that this buffer appears */
212 kdev_t b_dev; /* device (B_FREE = free) */
```