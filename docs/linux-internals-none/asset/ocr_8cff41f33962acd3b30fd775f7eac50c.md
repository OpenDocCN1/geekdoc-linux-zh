# The Linux VM Manager

```
* last.
 *
 * These will be removed, but in the mean time, the SECURE_NOROOT
 * flag is set, uids don't grant privilege.
 */
extern inline int suer(void)
{
    if (!issecure(SECURE_NOROOT) && current->euid == 0) {
        current->flags |= PF_SUPERPRIV;
        return 1;
    }
    return 0;
}

extern inline int fsuer(void)
{
    if (!issecure(SECURE_NOROOT) && current->fsuid == 0) {
        current->flags |= PF_SUPERPRIV;
        return 1;
    }
    return 0;
}

/*
 * capable() checks for a particular capability.
 * New privilege checks should use this interface, rather than suer() or
 * fsuer(). See include/linux/capability.h for defined capabilities.
 */
extern inline int capable(int cap)
{
#if 1 /* ok now */
    if (cap_raised(current->cap_effective, cap))
#else
    if (cap_is_fs_cap(cap) ? current->fsuid == 0 : current->euid == 0)
#endif
    {
        current->flags |= PF_SUPERPRIV;
        return 1;
    }
    return 0;
}

/*
 * Routines for handling mm_structs
 */
extern struct mm_struct * mm_alloc(void);

extern struct mm_struct * start_lazy_tlb(void);
extern void end_lazy_tlb(struct mm_struct *mm);

/* mmdrop drops the mm and the page tables */
extern inline void FASTCALL(__mmdrop(struct mm_struct *));
static inline void mmdrop(struct mm_struct * mm)
```