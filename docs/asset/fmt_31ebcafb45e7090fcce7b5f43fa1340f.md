
```c
arch/i386/asm/fault.c
473 valloc_fault:
  int index = pgd_index(address);
  pgd_t *pgd = *pgd_k;
  pmd_t *pmd = *pmd_k;
  pte_t *pte = *pte_k;
```

```c
asm(movl %%cr3,%0*="r" (pgd));
pgd = index + (pgd_t *)va(pgd);
pgd_k = init_mm.pgd + index;
```

```c
491 if (!pgd_present(*pgd_k))
    goto no_context;

pmd = pmd_offset(pgd, address);
pmd_k = pmd_offset(pgd_k, address);
if (!pmd_present(*pmd_k))
    goto no_context;
set_pmd(pmd, *pmd_k);

pte_k = pte_offset_kernel(pmd_k, address);
506 if (!pte_present(*pte_k))
507 goto no_context;
508 return;
509 }
```

#### 第 473-509 行

当前进程的页全局目录（通过 `cr3` 引用）被保存在变量 `pgd` 中，内核页全局目录由 `pgd_k` 引用（同样适用于 `pmd` 和 `pte` 变量）。如果违规地址在内核分页系统中无效，代码跳转到 `no_context:` 标签。否则，当前进程使用内核 `pgd`。

`vmalloc_fault:`

![](img/6525157588f931c50a65c5a42af9a432_270_0.png)

图 4.16

标签 `vmalloc_fault`

现在，我们看 `good_area:` 标签。此时，我们知道持有违规地址的内存区域存在于进程空间内。现在，我们需要确保访问权限是正确的。图 4.17 显示了流程：

```c
arch/i386/mm/fault.c
good_area:
info_code = SEGV_ACCERR;
write = 0;
switch (error_code & 3) {
default: /* 3: 写, 存在 */
/* fall through */ /* 写, 不存在 */
case 2:
if ((vma->vm_flags & VM_WRITE))
goto bad_area;
write++;
break;
case 1: /* 读, 存在 */
goto bad_area;
case 0: /* 读, 不存在 */
if ((vma->vm_flags & (VM_READ | VM_EXEC)))
goto bad_area;
}
```

#### 第 294-309 行

如果页异常是由写内存访问引起的（回想，如果是这种情况，我们错误码中最左侧的位被设置为 1），我们检查内存区域是否可写。如果不可写，则权限不匹配，我们跳转到标签 `bad_area:`。如果是可写的，我们穿透 `switch` 语句，并最终调用 `handle_mm_fault()`，并将局部变量 `write` 设置为 1。

#### 第 305-309 行

如果页异常是由读或执行访问引起的且该页存在，我们跳转到 `bad_area:`，因为这构成了明显的权限违规。如果页不存在，我们检查内存区域是否具有读取或执行权限。如果不具有，我们跳转到 `bad_area:`，即使获取了该页，权限也不允许该操作。如果具有，我们跳出 `switch` 语句，并最终调用 `handle_mm_fault()`，并将局部变量 `write` 设置为 0。

## 4.10 页缺异常

`good_area:`

![](img/6525157588f931c50a65c5a42af9a432_272_0.png)

图 4.17

标签 `good_area`

以下标签标记了当权限检查通过时，我们回穿透执行的代码。它被恰地命名为 `survive`（生存）：

```
arch/i386/mm/fault.c
survive:
318  switch (handle_mm_fault(mm, vma, address, write)) (
    case VM_FAULT_MINOR:
        tsk->min_flt++;
        break;
    case VM_FAULT_MAJOR:
        tsk->maj_flt++;
        break;
    case VM_FAULT_SIGBUS:
        goto do_sigbus;
    case VM_FAULT_OOM:
        goto out_of_memory;
329  default:
        BUG();
}
```

#### 第 318–329 行

调用 `handle_mm_fault()` 函数时传入了当前内存描述符 (`mm`)、违规地址的描述符、`address`，以及访问是读取/执行还是写入。`switch` 语句会在我们在处理异常失败时捕获错误，从而确保我们能够优雅地退出。

以下代码片段描述了 `bad_area` 和 `bad_area_no_semaphore` 标签的执行流。当我们跳转到此点时，我们知道以下情况之一：

- 1. 产生页异常的地址不在进程地址空间内，因为我们搜索了它的内存区域但没有找到匹配的区域。
- 2. 产生页异常的地址不在进程地址空间内，且包含该地址区域无法增长以容纳它。
- 3. 产生页异常的地址在进程地址空间内，但内存区域的权限与我们想要执行的操作不匹配。

现在，我们需要确定该访问是否来自内核态。以下代码和图 4.18 展示了这些标签的执行流：

```
arch/i386/mm.fault.c
348 bad_area:
349 up_read(&mm->mmap_sem);
350
351 bad_area_nosemaphore:
352 /* 用户态访问仅导致 SIGSEGV */
353 if (error_code & 4) {
354 if (is_prefetch(regs, address)) {
355 return;
356 }
357 tsk->thread.cr2 = address;
358 tsk->thread.error_code = error_code;
359 tsk->thread.trap_no = 14;
360 info.si_signo = SIGSEGV;
361 info.si_errno = 0;
362 /* info.si_code 在上方已设置 */
363 info.si_addr = (void *)address;
364 force_sig_info(SIGSEGV, &info, tsk);
365 return;
366 }
```

## 4.10 页缺异常

#### 第 348 行

`up_read()` 函数释放了进程内存描述符信号量的读锁。注意，只有在对内存描述符信号量加上读锁并遍历其内存区域以检查我们的地址是否在进程地址空间之后，我们才跳转到 `bad_area` 标签。否则，我们会跳转到 `bad_area_nosemaphore` 标签。两者的唯一区别在于是否释放信号量的读锁。

#### 第 351–353 行

由于地址不在地址空间中，我们现在检查错误是否是在用户态下生成的。如果你还记得表 4.7，错误代码值 4 表示错误发生在用户态。

#### 第 354–366 行

我们已经确定错误发生在用户态，因此我们发送了 `SIGSEGV` 信号（中断 14）。

#### `bad_area:` 

![](img/6525157588f931c50a65c5a42af9a432_274_0.png)

图 4.18

标签 `bad_area`

以下代码片段描述了 `no_context` 标签的执行流。当我们跳转到此点时，我们知道以下情况之一：

- 其中一个页表缺失。
- 内存访问并非在内核态下完成。

图 4.19 展示了 `no_context` 标签的流程图：

```
arch/i386/mm/fault.c
388   no_context:

390   if (fixup_exception(regs))
      return:

432   die("Oops", regs, error_code);
      bust_spinlocks(0);
      do_exit(SIGKILL);
```

#### 第 390 行

`fixup_exception()` 函数使用传入的 `eip` 在异常表中查找违规指令。如果指令在表中，则它在编译时已经内置了“隐藏”的异常处理代码。页异常处理器 `do_page__fault()` 使用异常处理代码作为返回地址并跳转到那里。代码随后可以标记错误。

#### 第 432 行

如果异常表中没有违规指令的条目，跳转到 `no_context` 的代码最终会导致 oops 屏幕转储（screen dump）。

`no_context:`
