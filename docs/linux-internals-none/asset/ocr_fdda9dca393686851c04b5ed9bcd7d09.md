```
800\t\t\tif ((p)->p_osptr) \\
801\t\t\t\t(p)->p_osptr->p_ysptr = (p)->p_ysptr; \\
802\t\t\tif ((p)->p_ysptr) \\
803\t\t\t\t(p)->p_ysptr->p_opstr = (p)->p_osptr; \\
804\t\t\telse \\
805\t\t\t\t(p)->p_pptr->p_cptr = (p)->p_osptr; \\
806\t\t} while (0)
807
808\t#define SET_LINKS(p) do { \\
809\t\t(p)->next_task = &init_task; \\
810\t\t(p)->prev_task = init_task.prev_task; \\
811\t\tinit_task.prev_task->next_task = (p); \\
812\t\tinit_task.prev_task = (p); \\
813\t\t(p)->p_ysptr = NULL; \\
814\t\tif (((p)->p_osptr = (p)->p_pptr->p_cptr) != NULL) \\
815\t\t\t(p)->p_osptr->p_ysptr = p; \\
816\t\t(p)->p_pptr->p_cptr = p; \\
817\t} while (0)
818
819\t#define for_each_task(p) \\
820\t\tfor (p = &init_task ; (p = p->next_task) != &init_task ; )
821
822\tstatic inline void del_from_runqueue(struct task_struct \* p)
823\t{
824\t	nr_running--;
825\t\tlist_del(&p->run_list);
826\t\tp->run_list.next = NULL;
827\t}
828
829\textern inline int task_on_runqueue(struct task_struct \*p)
830\t{
831\t\treturn (p->run_list.next != NULL);
832\t}
833
834\textern inline void unhash_process(struct task_struct \*p)
835\t{
836\t\tif (task_on_runqueue(p)) BUG();
837\t\twrite_lock_irq(&tasklist_lock);
838\t\tnr_threads--;
839\t\tunhash_pid(p);
840\t\tREMOVE_LINKS(p);
841\t\twrite_unlock_irq(&tasklist_lock);
842\t}
843
844\tstatic inline int task_lock(struct task_struct \*p)
845\t{
846\t\tdown(&p->exit_sem);
847\t\tif (p->p_pptr)
848\t\t\treturn 1;
849\t\t/* He's dead, Jim. You take his wallet, I'll take the triceror... */
850\t\tup(&p->exit_sem);
851\t\treturn 0;
852\t}
```