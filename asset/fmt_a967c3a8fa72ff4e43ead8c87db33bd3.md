
```c
289      read_lock_bt(&table->lock);
290      IP_NF_ASSERT(table->hooks & (1 << __hook));
291      table_base = (void *)table->private->entries
              + OFFSET_OFFSET(table->private,
              cpu_max_map(smp_processor_id(cpu)));
294      e = get_entry(table_base, table->private->hook_entry[]);

310      back = get_entry(table_base, table->private->underflow[hook]);
311      do {
312          IP_NF_ASSERT(e);
313          IP_NF_ASSERT(hook);
              (*packet)->offset = e->nfcache;
              if (packet_match(ip, in, outdev, &e->ip, offset)) {
                  struct ipt_target *target;
                  if (IPT_MATCH_ITERATE(e, do_match,
                              *target, in,
                              offset, protohdr,
                              data, &hdlen) != 0) {
                      goto match;
                  }
323      }
330      t = ipt_get_target(e);
331      if (t->u.kernel_target->target) {
332          int v;
333          v = (struct)((struct ipt_standard_target *)t->kernel_target)->verdict);
334          if (v < 0) {
335              /* 出栈? */
336              if (v == IPT_RETURN) {
337                  verdict = (unsigned int)v - 1;
                  break;
339              }
          e = back;
          back = get_entry(table_base,
                            back->next_from);
343          continue;
344      if (table_base + v + e->next_offset) {
345          t = (void *)(v + e->next_offset);
347      }
348      struct ipt_target *next;
349      next = (void *)(v + e->next_offset);
350      v = next_from;
351      v = (void *)back->table_base;
353      back = next;

355
356      e = get_entry(table_base, v);
357      } else {
364          verdict = t->u.kernel_target->target(psksb,
                               look,
                               in,
                               out,
                               t->data,
                               userdata);
382      ip = (*psksb)->nh.ip;
383      protohdr = (u_int32_t *)ip + ip->ihl;
384      data = (*psksb)->len - ip->ihl * 4;

386      if (verdict == IPT_CONTINUE) {
387          e = next->*" + v + e->next_offset;
388      else
389          /* 判决 */
390          break;
391      }
```

cs 16.38a. `ipt_do_table()`.

`net/ipv4/netfilter/ip_tables.c` `ipt_do_table()` 续。

```c
} else {
    no_match:
        e = (void *)e + e->next_offset;
} while (hotdrop);

read_unlock_bh(&table->lock);
....
if (hotdrop)
    return NF_DROP;
else return verdict;
```

cs 16.38b. `ipt_do_table`(续).

```c
include/linux/netfilter_ipv4/tables.h
292 void static __inline__ struct ipt_entry *
293 ipt_get_target(struct ipt_entry *e)
294 [
295 return (void *)e + e->target_offset;
```

cs 16.39. `ipt_get_target()`.

一个规则的特定目标或标准目标。在规则不匹配的情况下，我们需要跳转到某些不同的链进行过滤。标准目标除了目标对象 (`ipt_entry_target`) 之外，还有一个判决字段。一点，标准目标没有为其 `ipt_target` 对象初始化判决回调程序。我们检查第 330 行的匹配是否为标准目标。如果是，我们需要处理后续操作的标准判决字段。如果判决值为负值，则有两种可能：

- 1. 我们获取最终判决。
- 2. 判决为 `IPT_RETURN`。

在前一种情况下，我们返回这个最终判决。在后一种情况下，我们需要跳转回标准目标。

# 17 NET SOFTIRQ

中断处理分为两个部分。较小部分在中断处理程序（`interrupt handler`）中完成，大部分部分或称为下半部（`lower half`）则被推迟到安全的时间以最小的延迟进行处理。这样做是为了避免较长的中断延迟。在中断处理程序执行期间，中断会被禁用。一旦中断处理完成，中断就会被启用。如果我们在中断处理程序中花费过多的时间，中断延迟将会很高。

早期的 Linux 内核版本 2.2 及以下版本实现了下半部框架（`bottom-half framework`）来处理大部分中断。它在单 CPU 机器上运行良好，因为执行下半部时需要持有大的下半部锁（`bottom-half lock`）。在 SMP（多处理器）机器上，该框架会导致每个 CPU 在执行下半部时的串行访问，因为我们需要持有锁来执行下半部。该框架无法在 SMP 机器上扩展。

为了提高下半部执行的可扩展性，该框架经过修改，以便在 SMP 机器上更好地扩展扩展。新框架被称为 `softirQs`。`SoftIRQs` 设计为在多个 CPU 上并行运行。此外，同一个 `softIRQ` 可以同时在不同的 CPU 上并行运行。由于每个 CPU 维护各自的数据，因此可以在每个 CPU 上独立地抛起 `softIRQs`。

并不是每个中断事件都有独立的 `softIRQ`。网络有两个下半部，一个用于 Tx（发送），一个用于 Rx（接收）中断。其他中断事件将它们的下半部注册为高优先级或低优先级的任务。每个种任务有高优先级和低优先级两个 `softIRQs`。任务（`tasklet`）的特点是同一时间只能在一个 CPU 上执行，这意味着特定的 `tasklet` 每次只能在一个 CPU 上运行。在本章中，我们将学习更多关于 `softIRQs` 及其执行机制的知识。

## 17 NET SoftIRQ

![](img/b3f231108facab5be0138b2cfd3f681a_687_0.png)

图 17.1. Tx net softIRQ。

## 17.1 为什么需要 NET SOFTIRQS，以及我们如何触发它们？
