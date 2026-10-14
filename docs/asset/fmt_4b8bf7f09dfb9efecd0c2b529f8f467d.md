
```c
178 {
179    unsigned long flags;
180    spin_lock_irsave(&timerlist_lock, flags);
181    if (timer_pending(timer))
182        goto bug;
183    internal_add_timer(timer);
184    spin_lock_irrestore(&timerlist_lock, flags);
185    return;
186 bug:
187    spin_lock_irrestore(&timerlist_lock, flags);
188    printk("bug: kernel timer added twice at %p.\n",
189    builtin_return_address(0));
190 }
```

图 15.30 将定时添加到列表

181–182 函数在 164 行声明的 `timerlist_lock` 自旋锁保护下执行所有工作。中断安全的自旋锁宏来自节 12.8。

182–183 函数检查是否已经插入。`timer_pending()` 函数来自第 15.3.2.7 节。如果它已经在列表中，说明出了问题。

184 如果不在列表中，则会被插入（见第 15.3.2.4 节）。

187 如果作为参数提供的 `timer_list` 结构已经在列表中，则执行此错误处理代码。

188 返回自旋锁。

189 打印一条错误消息，给出栈上的返回地址，即调用此处的函数地址。

# 15.3.2.3 修改定时器的值

有时，在定时器进入列表后，需要更改其过期时间。图 15.31 所示函数位于 `kernel/timer.c`，将 `timer` 参数指定的定时器值更改为 `expires` 参数的值。它将定时器从列表当前位置移除，并插入到与其新值合适的位置。

```c
201 int mod_timer(struct timer_list *timer, unsigned long expires)
202 {
203    int ret;
204    unsigned long flags;
205
206    spin_lock_irsave(&timerlist_lock, flags);
207    timer->expires = expires;
208    ret = detach_timer(timer);
```

# 定时中断

```c
209 internal_add_timer(timer);
210 spin_unlock_irrestore(&timerlist_lock, flags);
211 return ret;
212 }
```

图 15.31 修改定时器的值

206–210 定时列表上的所有操作都在 `timerlist_lock` 自旋锁的保护下进行。

207 它更改 `timer_list` 结构中的相应字段以反映新的过期时间。

208 它从列表中分离定时器（见第 15.3.2.6 节）。此处未检查返回值（1 为成功，0 为失败）。

209 然后将时间添加到列表中新的（适当的）位置（见第 15.3.2.4 节）。即使上一行未能分离定时器也是如此的。

210 它释放自旋锁。

211 函数返回从 `detach_timer()` 获取的值，该值应该是成功 1，失败 0（如果列表中没有此类结构）。

# 15.3.2.4 工作将定时器添加到适当列表

定时器根据请求的超时时间被放入五个列表之一。图 15.32 所示函数位于 `kernel/timer.c`，确定哪个列表是合适的并将结构插入该列表。它由三个不同的函数 `add_timer()`、`mod_timer()` 和 `cascade_timers()` 调用——这些在本节中描述。在每种情况下，调用者都持有 `timerlist_lock` 自旋锁。

# 事件定时器

```c
141      else else if (idx<1<< (TVR_BITS + 3* TVN_BITS)) {
142          int i = (expires >> (TVR_BITS + 2* TVN_BITS)) &TVN_MASK;
143          vec = tv4.vec+i;
144      } else if ((signed long) idx<0) {
148          vec = tv1.vec+tv1.index;
149      } else if (idx <= 0xffffffff) {
150          int i = (expires>>TVR_BITS + 3* TVN_BITS)) &TVN_MASK;
151          vec = tv5.vec+i;
152      } else {
154          INIT_LIST_HEAD(&timer->list);
155          return;
156      }
160      list_add(&timer->list, vec->prev);
161  }
```

**图 15.32** 为定时器请求选择合适的列表

`timer_jiffies` 变量是 `run_timer_list()` 上次运行时当前时间（jiffies）的拷贝。

此行获取了该定时器到期时间的本地拷贝。

`timer_jiffies` 变量在第 121 行定义。它是 `run_timer_list()` 上次运行时当前时间（jiffies）的拷贝。当它运行时，它将从该时间开始检查过期的定时器，因此插入的这个新定时器（idx）的剩余间隔是从那时开始计算的。

`TVR_SIZE` 定义为 256（见第 15.3.1.2 节）。如果间隔内的滴答少于此值，则将其插入定时器列表 1。

`TVR_MASK` 为 1111 1111（见第 15.3.1.2 节），因此它屏蔽了 `expires` 的所有低 8 位。这些位足以唯一标识应该将定时器插入到 `tv1` 中 256 个列表中的哪一个。

为此特定 `timer_list` 结构选择的列表头部来自 `tv1` 中的条目 i；然后我们跳转到第 160 行。

`TVR_BITS` + `TVN_BITS` = 8 + 6 = 14，因此 14 是 1000 0000 0000 0000 或 0x400，或 1k。如果间隔大于 256 加 55 但小于 16 个滴答，则选择定时器列表 2。

`TVR_BITS` 为 8，因此它划分了 `expires`。该向量没有像 `tv1` 那样为每个滴答提供一个列表。每个列表将将在 256 个滴答范围内过期的定时器分组，屏蔽了所有低 6 位。这些位足以唯一标识应该将定时器插入到 `tv2` 中 64 个列表中的哪一个。

这从 `tv1` 中的 i 选择了列表头部。`tv2` 中的每个列表其 `expires` 字段中具有 256 个滴答范围的定时器；然后我们跳转到第 160 行。

# 定时器中断

138 将 1 左移 20 位得到 0x100000 或 1M。如果间隔在 16k 到 1M 滴答之间，则定时器被插入 `tv2`。

139 这将 `expires` 除以 16k 并屏蔽除低 6 位以外的所有位。该向量中的每个列表将 16k 个滴答范围内过期的定时器分组。

140 这选择了由 `tv3` 中的 i 领头的列表；然后我们跳转到第 160 行。

141–143 如果间隔在 1M 到 64M 滴答之间，则此处将 `expires` 除以 1M 并选择由 `tv4` 中的 i 领头的列表；然后我们跳转到第 160 行。

144 如果定时器被设置为在过去触发，则可能发生此情况。在这种情况下，`vec` 将被连续赋值直到最后，而这就是确定值。似乎这个测试应该先进行。

148 所选的列表是下一个过期的定时器，即由索引指向的 `tv1` 中的列表；然后我们跳转到第 160 行。

149 如果间隔在 32 位内，则此处将 `expires` 除以 64M 并选择由 `tv5` 中的 i 领头的列表；然后我们跳转到 160。

152 这仅发生在具有 64 位连接的架构上，因此与 PC 无关。`INIT_LIST_HEAD()` 见第 4.3.1 节。它初始化 `struct timer_list` 结构指向自身并返回。

160 最后，这将定时器插入所选列表的末尾；`vec->prev` 指向列表的末尾。`list_add()` 函数见第 4.3.2 节。

# 15.3.2.5 从列表中删除定时器

当定时器过期时，它会从列表中移除，但也可以在过期之前被移除。图 15.33 所示的函数位于 `kernel/timer.c`，用于这两种情况。
