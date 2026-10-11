The `rmb()` method provides a read memory barrier. It ensures that no loads are re-ordered across the `rmb()` call. That is, no loads prior to the call will be reordered to after the call, and no loads after the call will be reordered to before the call.

The `wmb()` method provides a write barrier. It functions in the same manner as `rmb()`, but with respect to stores instead of loads—it ensures no stores are reordered across the barrier.

The `mb()` call provides both a read barrier and a write barrier. No loads or stores will be reordered across a call to `mb()`. It is provided because a single instruction (often the same instruction used by `rmb()`) can provide both the load and store barrier.

A variant of `mb()`, `read_barrier_depends()`, provides a read barrier but only for loads on which subsequent loads depend. All reads prior to the barrier are guaranteed to complete before any reads after the barrier that depend on the reads prior to the barrier. Got it? Basically, it enforces a read barrier, similar to `rmb()`, but only for certain reads—those that depend on each other. On some architectures, `read_barrier_depends()` is much quicker than `rmb()` because it is not needed and is, thus, a no-op.

Let's consider an example using `mb()` and `rmb()`. The initial value of a is one, and the initial value of b is two.

| Thread 1 | Thread 2 |
| :--- | :--- |
| a = 3; | — |
| mb(); | — |
| b = 4; | c = b; |
| — | rmb(); |
| — | d = a; |

Without using the memory barriers, on some processors it is possible for c to receive the new value of b, whereas d receives the old value of a. For example, c could equal four (what you'd expect), yet d could equal one (not what you'd expect). Using the `mb()` ensured that a and b were written in the intended order, whereas the `rmb()` insured c and d were read in the intended order.

This sort of reordering occurs because modern processors dispatch and commit instructions out of order, to optimize use of their pipelines. What can end up happening in the previous example is that the instructions associated with the loads of b and a occur out of order. The `rmb()` and `wmb()` functions correspond to instructions that tell the processor to commit any pending load or store instructions, respectively, before continuing.

Let's look at a similar example, but one that uses `read_barrier_depends()` instead of `rmb()`. In this example, initially a is one, b is two, and p is &b.