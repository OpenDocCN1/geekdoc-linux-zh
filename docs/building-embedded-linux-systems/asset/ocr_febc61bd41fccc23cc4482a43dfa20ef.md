```
xnpod_suspend_thread(&task->threadbase, XNSUSP_XN_INFINITE, XN_RELATIVE, NULL);   

if (task == pso_current_task()) &&
xthread_test_info(&task->threadbase, XNBREAK))
ret = -EINTR;

unlock_and_exit:

xlock_put_irqrestore(&mlock, s);

return ret;
```

As the code sample shows, the Xenomai nucleus handles the most complex part of the system call by carrying out the actual suspension and maintaining task state information so that the p5OS emulator can decide what has to be done next. The rest of the code is just window-dressing around the **threadbase** anchor object, which is the thread-specific data structure exported by the nucleus to model real-time tasks.

The example that follows was taken from the VRTX emulator. It implements the *sc_pend()* call from the *mailbox* IPC, which makes the caller wait on a memory cell until some nonzero data has been written to it (this is a timed service, so the caller may specify a timeout value):

```
char *sc_pend(char **mbxop, long timeout, int *errp)
{
    char *msg = NULL;
    vrtxtask_t *task;
    vrtxmb_t *mb;
    spl_t s;

    /* Protect from preemption in the Xenomai domain. */
    xlock_get_irqsave(&mlock, s);

    /* Find out our control block for this mailbox. */
    mb = mb_map(mbxop);

    if (!mb) {
        *errp = ER_NOSB;
        goto unlock_and_exit;
    }

    if (mb->msg != NULL)
    /*
     * Something has been written in there already, return
     * that value without blocking the caller.
     */
        goto done;

    /* May we block the calling context? */
    if (xnpod_unlockable_p()) {
        *errp = -EPERM;
        goto unlock_and_exit;
```