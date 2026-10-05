

## 724 TCP/IP 和 Linux 协议实现

```c
185 }
186 write_unlock(&qdisc_mod_lock);
187 return err;
188 }
```

图 9.91 调度 API–通过句柄查找队列：linux/net/sched/sch_api.c。

```c
190 /* 我们知道 handle。在所有附加到设备的 qdisc 中查找 qdisc
191 (根 qdisc, 所有的子节点, 节点的子节点等)
192 */
193 struct Qdisc *qdisc_lookup(struct net_device *dev, u32 handle)
194 {
195 
196 struct Qdisc *q;
197 
198 for (q = dev->qdisc_list; q = q->next) {
199 if (q->handle == handle)
200 return q;
201 
202 return NULL;
203 }
204 
205 struct Qdisc *qdisc_leaf(struct Qdisc *p, u32 classid)
206 {
207 unsigned long cl;
208 struct Qdisc *leaf;
209 struct Qdisc_class_ops *cops = p->ops->cl_ops;
210 
211 if (cops == NULL)
212 return NULL;
213 cl = cops->get(p, classid);
214 
215 if (cl == 0)
216 return NULL;
217 leaf = cops->leaf(p, cl);
218 cops->put(p, cl);
219 return NULL;
220 }
```

图 9.92 调度 API–通过名称查找队列：linux/net/sched/sch_api.c。

```c
224 struct Qdisc_ops *qdisc_lookup_ops(struct rattr *kind)
225 {
226 struct Qdisc_ops *q = NULL;
227 
228 if (kind) {
229 read_lock(&qdisc_mod_lock);
230 for (q = qdisc_base; q = q->next) {
231 if (rattr_strcmp(kind, q->id) == 0)
232 break;
```

```c
}
read_unlock(&qdisc_mod_lock);
}
return q;
}
```

## 9.93 调度 API–通过速率完成队列：linux/net/sched/sch_api.c。

```c
struct qdisc_rate_table *qdisc_get_rtab(struct tc_ratespec *r, struct rtattr *tab)
{
    struct qdisc_rate_table *rtab;

    for (rtab = qdisc_rtab_list; rtab; rtab = rtab->next) {
        if (memcmp(rtab->rate, r, sizeof(struct tc_ratespec)) == 0) {
            rtab->refcnt++;
            return rtab;
        }
    }

    if (tab == NULL || r->rate == 0 || r->cell_log == 0 || RTA_PAYLOAD(tab) != 1024) {
        return NULL;
    }

    rtab = kmalloc(sizeof(*rtab), tab, GFP_KERNEL);
    if (rtab) {
        rtab->rate = *r;
        rtab->refcnt = 1;
        memcpy(rtab->data, RTA_DATA(tab), 1024);
        rtab->next = qdisc_rtab_list;
        qdisc_rtab_list = rtab;
    }
    return rtab;
}
```

## 9.94 调度 API–释放速率表项：linux/net/sched/sch_api.c。

```c
void qdisc_put_rtab(struct qdisc_rate_table *rtab, struct **rtab);
{
    struct qdisc_rate_table *rtab, **rtab;
    if (rtab || --rtab->refcnt) {
        return;
    }

    for (rtab = &qdisc_rtab_list; *rtab != NULL; rtab = &rtab->next) {
        if (*rtab == *rtab) {
            *rtab = rtab->next;
            free(rtab);
            return;
        }
    }
}
```

## 图 9.95 调度 API–将队列分配到唯一的句柄：linux/net/sched/sch...

```c
u32 qdisc_alloc_handle(struct net_device *dev)
{
    int i = 0x10000;
    static u32 authandle = TC_H_MAKE(0x10000, 0);

    do {
        authandle = TC_H_MAKE(i++, 0);
        if (!qdisc_lookup(dev, authandle))
            return authandle;
    } while (i < 0x20000);

    return 0;
}

void qdisc_free_handle(u32 *handle);
}
```

## 图 9.96 调度 API–将队列到设备：linux/net/sched/sch...

```c
/* 挂载队列到设备 */
static struct Qdisc *
dev_graft(struct net_device *dev, struct Qdisc *new)
{
    struct Qdisc *old = NULL;

    if (new) {
        read_lock(&qdisc_mod_lock);
        for (old = dev->qdisc_list; old; old = old->next) {
            if (old->handle == new->handle) {
                break;
            }
        }
        read_unlock(&qdisc_mod_lock);

        if (old) {
            qdisc_free_handle(new->handle);
        } else {
            new->next = dev->qdisc_list;
            dev->qdisc_list = new;
        }
    }
    return new;
}
```

## 9.97 调度 API–将队列到类：linux/net/sched/sch_api.c。

（注：此处代码逻辑翻译）

## 9.98 调度 API–分配并初始化新队列：linux/net/sched/api.c。

```c
/*
 分配并初始化队列。
 参数通过 opt 传递。 */
static struct Qdisc *
qdisc_create(struct net_device *dev, u32 handle, struct rtattr *tca, int *errp)
{
    int err;
    struct rtattr *kind = tca[TCA_KIND-1];
    struct Qdisc *sch = NULL;
    struct Qdisc_ops *ops;
    size_t size;

    ops = qdisc_lookup_ops(kind);
#ifdef CONFIG_FIO
    if (ops == NULL && tca[TCA_KIND-1] != NULL) {
        char module_name[4 + IFNAMSIZ];
        if (RTA_PAYLOAD(kind) < IFNAMSIZ) {
            sprintf(module_name, "sch_%s", (char*)RTA_DATA(kind));
            request_module(module_name);
            ops = qdisc_lookup_ops(kind);
        }
    }
#endif

    err = -EINVAL;
    if (ops == NULL)
        goto err_out;

    size = sizeof(*sch) + ops->priv_size;

    sch = kmalloc(size, GFP_KERNEL);
    err = -ENOMBUFS;
    if (!sch)
        goto err_out;

    /* ... 解决与模块卸载的竞争条件 */
    err = -EINVAL;
    if (ops != qdisc_lookup_ops(kind))
        goto err_out;

    memset(sch, 0, size);

    skb_queue_head_init(&sch);

    if (handle == TC_H_INGRESS)
        sch->flags |= TCQ_F_INGRESS;

    sch->ops = ops;
    sch->enqueue = ops->enqueue;
    sch->dequeue = ops->dequeue;
    sch->dev = dev;
    atomic_set(&sch->refcnt, 1);
    sch->lock = &dev->queue_lock;
    if (handle == 0) {
        handle = qdisc_alloc_handle(dev);
        err = -ENOMEM;
        if (!handle)
            goto err_out;
    }
    err = 0;
    return sch;

err_out:
    if (sch) {
        kfree(sch);
    }
    *errp = err;
    return NULL;
}
```

