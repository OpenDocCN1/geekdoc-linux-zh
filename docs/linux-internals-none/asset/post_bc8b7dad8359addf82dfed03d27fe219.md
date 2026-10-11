
# The Linux Process Model

```c
cap_set_full(bprm->cap_effective);
}

/* Only if pP' is _not_ a subset of pP, do we consider there
 * has been a capability related "change of capability". In
 * such cases, we need to check that the elevation of
 * privilege does not go against other system constraints.
 * The new Permitted set is defined below -- see (***) . */
{
    kernel_cap_t working =
        cap_combine(bprm->cap_permitted,
        cap_intersect(bprm->cap_inheritable,
                current->cap_inheritable));

    if (!cap_issubset(working, current->cap_permitted)) {
        cap_raised = 1;
    }
}

if (id_change || cap_raised) {
    /* We can't suid-execute if we're sharing parts of the executable */
    /* or if we're being traced (or if suid execs are not allowed)    */
    /* (current->mm->mm_users > 1 is ok, as we'll get a new mm anyway)  */
    if (IS_NOSUID(inode)
            must_not_trace_exec(current)
        || (atomic_read(&current->fs->count) > 1)
        || (atomic_read(&current->sig->count) > 1)
        || (atomic_read(&current->files->count) > 1)) {
        if (id_change && !capable(CAP_SETUID))
            return -EPERM;
        if (cap_raised && !capable(CAP_SETPCAP))
            return -EPERM;
    }
}

memset(bprm->buf,0,sizeof(bprm->buf));
return read_exec(bprm->dentry,0,bprm->buf,128,1);
}
```

- 2. Set up the arguments to be passed to the newly called program and its argument (argc,argv,envp).
- 3. Select the appropriate binary handler according to the binary file's magic number. As we saw in earlier chapters, Linux is able to execute a variety of binary formats, including a.out, ELF, Java, iBCS, and EM86. The function `search_binary_handler` recognizes the binary image according to the magic number contained in the header information.

Here is the function `search_binary_handler` from `fs/exec.c`:

```c
int search_binary_handler(struct linux_binprm *bprm,struct pt_regs *regs)
{
    int try,reval=0;
    struct linux_binfmt * fmt;

#ifdef __alpha__
/* handle /sbin/loader... */
    {
        struct exec * eh = (struct exec *) bp_rm->buf;
        struct linux_binprm bprm_loader;

        if (!bprm->loader && eh->fh.f_fmagic == 0x183 &&
            (eh->fh.f_flags & 0x3000) == 0x3000)
        {
            int i;
            char * dynloader[] = { "/sbin/loader" };
            struct dentry * dentry;

            lock_kernel();
            dput (bprm->dentry);
            unlock_kernel();
            bprm->dentry = NULL;

            bprm_loader.p = PAGE_SIZE*MAX_ARG_PAGES-sizeof(void *);
            for (i = 0 ; i < MAX_ARG_PAGES ; i++)    /* clear page-table */
                bprm_loader.page[i] = NULL;

            lock_kernel();
            dentry = open_namei(dynloader[0], 0, 0);
            unlock_kernel();
            retval = PTR_ERR(dentry);
            if (IS_ERR(dentry))
                return retval;
            bprm->dentry = dentry;
            bprm->loader = bprm_loader.p;
            retval = prepare_binprm(bprm);
            if (retval<0)
                return retval;
            /* should call search_binary_handler recursively here,
               but it does not matter */
        }
    }
    #endif
    for (try=0; try<2; try++) {
        for (fmt = formats ; fmt ; fmt = fmt->next) {
            int (*fn)(struct linux_binprm *, struct pt_regs *) = fmt->load_binary;
            if (!fn)
                continue;
            retval = fn(bprm, regs);
            if (retval >= 0) {
                if (bprm->dentry) {
                    lock_kernel();
                    dput (bprm->dentry);
                    unlock_kernel();
                }
                bprm->dentry = NULL;
                current->did_exec = 1;
                return retval;
            }
            if (retval != -ENOEXEC)
                break;
            if (bprm->dentry) /* We don't have the entry anymore */
                return retval;
            if (retval != -ENOEXEC) {
                break;
                #ifdef CONFIG_KMOD
                } else {
                #define printable(c) (((c)=='\t') || ((c)=='\n') || (0x20<=(c) && (c)<=0x7e))
                char modname[20];
                if (printable(bprm->buf[0]) &&
                printable(bprm->buf[1]) &&
                printable(bprm->buf[2]) &&
                printable(bprm->buf[3]) {
                break; /* -ENOEXEC */
                sprintf(modname, "binfmt-%04x", *(unsigned short *)(&bprm->buf[2]));
                request_module(modname);
                }
                #endif
            }
    return retval;
}
```

- 4. Finally, control is passed over the binary image read in from the file.

Obviously, the *fork()*, *__clone()*, and *exec()* kernel functions have serious implications for the virtual memory manager. The VM has to set up the virtual address space for the new program. It does so by creating an exact copy of each VM page each time it is referenced. On reference, the addressing hardware generates a page fault (because it is a nonexistent VM address) and calls the VM code. The VM recognizes the situation and copy-creates the new page. We shall, however, have a much closer look at VM workings in the chapter on the Linux VM manager.

# Threads

In the last 10 years or so, there has been a general move from heavyweight processes to a threaded model. The reason is clear: the creation and maintenance of a full process with its own address space takes up a lot of time (in terms of milliseconds). Threads, instead, run within the same address space as the father process and therefore require much less time in creation. With the enormous importance of Web servers and the e-commerce wave, having efficient and responsive task creation and shutdown is a primary concern. In fact, for some time now, Web server developers have tried to include all programming functionality within a single address space. Apache, for instance, includes a Perl module to enable Web developers to execute Perl code without exiting the address space.

What's the difference between process and thread under Linux? And, more important, what is the difference from a scheduler's point of view? In short: nothing.

The only worthwhile difference between a thread and a process is that the threads share completely the same address space. All the threads run in the same address space so a context switch is basically just a jump from one location of code to another location of code.

The simple check to avoid the translation look-aside buffer (TLB)—the mechanism within the CPU that translates virtual memory addresses to real RAM addresses—flush and the memory manager context switch is found in linux/arch/i386/kernel/process.c:

```c
/* Re-load page tables */
{
  unsigned long new_cr3 = next->tss.cr3;
  if (new_cr3 != prev->tss.cr3)
    asm volatile("movl %0,%%cr3": :"r" (new_cr3));
}
```

The above check is in the core of the Linux kernel context switch. It checks if the address of the page-directory of the current process and the one of the to-be-scheduled-process are the same. If they are, it means they are sharing the same address space (or in other words, they are two threads) and the kernel avoids writing to the %cr3 register, so that the userspace page tables won't be invalidated. This happens because the cr3 register just contains the data to which the kernel would write (and writing to it would mean invalidating the TLB). With the above two-line check Linux defines a difference between a kernel process switch and a kernel thread switch. This is the only noteworthy difference.

Because there is no difference at all between threads and processes, the Linux scheduler is written in very clean code. Only a few places related to signal handling make differences between threads and processes. This is very much contrary to, say, Solaris where the process is greatly disadvantaged compared to the thread and lightweight processes. The code below finds a measurement on a Solaris server, an Ultra 2 desktop 167-MHz processor, running Solaris 2.6:

```
orion> ftime
Completed 100 forks
Avg. Fork Time: 1.137 milliseconds
```
