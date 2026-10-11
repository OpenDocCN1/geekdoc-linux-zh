```
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
```