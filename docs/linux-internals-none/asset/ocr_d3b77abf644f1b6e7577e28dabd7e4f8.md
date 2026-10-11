```
216 unsigned long rss, total_vm, locked_vm;
217 unsigned long def_flags;
218 unsigned long cpu_vm_mask;
219 unsigned long swap_cnt; /* number of pages to swap on next pass */
220 unsigned long swap_address;
221 /**
222 * This is an architecture-specific pointer: the portable
223 * part of Linux does not know about any segments.
224 */
225 void * segments;
226 };
227
228 #define INIT_MM(name) {
229 &init_mmmap, NULL, NULL,
230 swapper_pg_dir,
231 ATOMIC_INIT(2), ATOMIC_INIT(1), 1,
232 __MUTEX_INITIALIZER(name.mmmap_sem),
233 SPIN_LOCK_UNLOCKED,
234 0,
235 0, 0, 0, 0,
236 0, 0, 0,
237 0, 0, 0, 0,
238 0, 0, 0,
239 0, 0, 0, 0, NULL }
240
241 struct signal_struct {
242 atomic_t count;
243 struct k_sigaction action[_NSIG];
244 spinlock_t siglock;
245 };
246
247
248 #define INIT_SIGNALS {
249 ATOMIC_INIT(1), 
250 { {{0}}, }, 
251 SPIN_LOCK_UNLOCKED }
252
253 /**
254 * Some day this will be a full-fledged user tracking system.
255 * Right now it is only used to track how many processes a
256 * user has, but it has the potential to track memory usage etc.
257 */
258 struct user_struct;
259
260 struct task_struct {
261 /* these are hardcoded - don't touch */
262 volatile long state; /* -1 unrunnable, 0 runnable, >0 stopped */
263 unsigned long flags; /* per process flags, defined below */
264 int sigpending;
265 mm_segment_t addr_limit; /* thread address space:
266 0-0xBFFFFFFF for user-thread
267 0-0xFFFFFFFF for kernel-thread
268 */
269 struct exec_domain *exec_domain;
```