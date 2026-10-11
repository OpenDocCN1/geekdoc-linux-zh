```
    pid_ns->child_reaper = thread;
    return thread;
}

if (unlikely(pid_ns->child_reaper == father)) {
    write_unlock_irq(&tasklist_lock);
    if (unlikely(pid_ns == &init_pid_ns))
        panic("Attempted to kill init!");

    zap_pid_ns_processes(pid_ns);
    write_lock_irq(&tasklist_lock);
    /*
     * We can not clear ->child_reaper or leave it alone.
     * There may by stealth EXIT_DEAD tasks on ->children,
     * forget_original_parent() must move them somewhere.
     */
    pid_ns->child_reaper = init_pid_ns.child_reaper;
}
return pid_ns->child_reaper;
```

This code attempts to find and return another task in the process's thread group. If another task is not in the thread group, it finds and returns the _init_ process. Now that a suitable new parent for the children is found, each child needs to be located and reparented to _reaper_:

```
reaper = find_new_reaper(father);
list_for_each_entry_safe(p, n, &father->children, sibling) {
    p->real_parent = reaper;
    if (p->parent == father) {
        BUG_ON(p->ptrace);
        p->parent = p->real_parent;
    }
    reparent_thread(p, father);
}
```

ptrace_exit_finish() is then called to do the same reparenting but to a list of _ptraced_ children:

```
void exit_ptrace(struct task_struct *tracer)
{
    struct task_struct *p, *n;
    LIST_HEAD(ptrace_dead);

    write_lock_irq(&tasklist_lock);
    list_for_each_entry_safe(p, n, tracer->ptraced, ptrace_entry) {
        if (!__ptrace_detach(tracer, p))
            list_add(&p->ptrace_entry, &ptrace_dead);
```