```
854 
855 static inline void task_unlock(struct task_struct *p)
856 {
857         up(&p->exit_sem);
858 }
859 
860 #endif /* __KERNEL__ */
861 
862 #endif
```