```
```
640	/*
641	 * Routines for handling mm_structs
642	 */
643	extern struct mm_struct * mm_alloc(void);
644	
645	extern struct mm_struct * start_lazy_tlb(void);
646	extern void end_lazy_tlb(struct mm_struct *mm);
647	
648	/* mm_drop drops the mm and the page tables */
649	extern inline void FASTCALL(__mm_drop(struct mm_struct **));
650	static inline void mm_drop(struct mm_struct * mm)
651	{
652		if (atomic_dec_and_test(&mm->mm_count))
653			__mm_drop(mm);
654	}
655	
656	/* mmput gets rid of the mappings and all user-space */
657	extern void mmput(struct mm_struct *);
658	/* Remove the current tasks stale references to the old mm_struct */
659	extern void mm_release(void);
660	
661	/*
662	 * Routines for handling the fd arrays
663	 */
664	extern struct file ** alloc_fd_array(int);
665	extern int expand_fd_array(struct files_struct *, int nr);
666	extern void free_fd_array(struct file **, int);
667	
668	extern fd_set *alloc_fdset(int);
669	extern int expand_fdset(struct files_struct *, int nr);
670	extern void free_fdset(fd_set *, int);
671	
672	/* Expand files.  Return <0 on error; 0 nothing done; 1 files expanded,
673	 * we may have blocked.
674	 *
675	 * Should be called with the files->file_lock spinlock held for write.
676	 */
677	static inline int expand_files(struct files_struct *files, int nr)
678	{
679		int err, expand = 0;
680	#ifdef FDSET_DEBUG
681		printk(KERN_ERR __FUNCTION__ " %d: nr = %d\n", current->pid, nr);
682	#endif
683	
684		if (nr >= files->max_fdset) {
685			expand = 1;
686			if ((err = expand_fdset(files, nr)))
687				goto out;
688		}
689		if (nr >= files->max_fds) {
690			expand = 1;
691			if ((err = expand_fd_array(files, nr)))
692				goto out;
693		}
```
```