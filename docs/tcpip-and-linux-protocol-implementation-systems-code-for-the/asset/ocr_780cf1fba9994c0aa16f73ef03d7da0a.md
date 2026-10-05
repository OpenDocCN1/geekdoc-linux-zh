# Figure 9.1 Firewall classifier API–destroy classifier: linux/net/sched/cls_fw.c.

```
static void fw_destroy(struct tcf_proto *tp)
{
    struct fw_head *head = (struct fw_head*)xchg(&(kt->tp)->root, NULL);
    struct fw_filter *f;
    int h;

    if (head == NULL) {
        MOD_DEC_USE_COUNT;
        return;
    }

    for (h=0; h<256; h++) {
        while ((f=head->ht[h]) != NULL) {
            unsigned long cl;
            head->ht[h] = f->next;
            if ((cl = cls_set_class(&f->res.class, 0)) != 0)
                tp->q->ops->cl_ops->unbind_tcf(tp->q, cl);
            else
                #ifdef CONFIG_NET_CLS_POLICE
                tcf_policy_release(f->policy);
                #endif
            free(f);
        }
    }
    free(head);
    MOD_DEC_USE_COUNT;
}
```

# Figure 9.2 Firewall classifier API–delete classifier: linux/net/sched/cls_fw.c.

```
static int fw_delete(struct tcf_proto *tp, unsigned long arg)
{
    struct fw_head *head = (struct fw_head*)tp->root;
    struct fw_filter *f = (struct fw_filter*)arg;

    if (head == NULL || f == NULL) {
        return -EINVAL;
    }

    for (fp=head->ht[hash(f->id)]; fp = &(fp->fp)->next) {
        if (*fp == f) {
            unsigned long cl;

            tcf_tree_lock(tp);
            *fp = f->next;
            tcf_tree_unlock(tp);

            if ((cl = cls_set_class(&f->res.class, 0)) != 0)
                tp->q->ops->cl_ops->unbind_tcf(tp->q, cl);
            else
n                #ifdef CONFIG_NET_CLS_POLICE
                tcf_policy_release(f->policy);
                #endif
        }
    }
```