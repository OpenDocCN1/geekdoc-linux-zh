We could try to replace $Q$ with a counting semaphore (Section 7.8), but a better choice is to use another kind of signaling mechanism that POSIX Threads provides: condition variables. Here’s how they’re used in this example:

+   **Thread A**
+   
+   1. Read data [B]
+   2. Lock $M$ [b]
+   3. Put item on queue
+   4. cond_signal(C)
+   5. Unlock $M$
+   6. Goto step 1

+   **Thread B**
+   
+   1. Lock $M$ [b]
+   2. while (queue is empty) {
+      cond_wait(C, $M$) [B]
+      }
+   3. Remove item; update database
+   4. Unlock $M$
+   5. Goto step 1

The second mutex, $Q$, is gone, and now there’s a condition variable, $C$. In Thread B, cond_wait waits until condition $C$ is signaled, which it is in Thread A’s step 4. But cond_wait has a special interaction with mutex $M$ (its second argument): The mutex must be locked when cond_wait is called. *It is unlocked during the waiting, and then relocked automatically when cond_wait returns*. That way there’s no possibility of a missed signal or of deadlock, both of which were defects in our earlier attempts. And, all the code in Thread B’s steps 2 and 3 is executed with $M$ locked, as it should be.

Why is cond_wait in a loop that tests whether the queue is empty, when condition $C$ gets signaled (by Thread A) only when the queue is nonempty? It’s because cond_wait, like any UNIX blocking system call, is subject to being interrupted (e.g., by the arrival of a traditional UNIX signal, such as SIGINT), in which case there might be a return with the queue still empty. A loop that tests the predicate (empty queue, in this case) ensures that we’ll go right back into cond_wait on such a spurious return. Because spurious returns are infrequent, the wasted CPU time is inconsequential.

Another reason for checking the queue before calling cond_wait is that cond_signal might have been called well before Thread B calls cond_wait, and a cond_signal with no thread waiting is discarded (not held pending). So, it’s important not to call cond_wait unless waiting is necessary, or the wait may be forever, even though the queue is nonempty.

Thus, to signal and wait for a condition, you need three things: a *condition variable*, a *mutex*, and a *predicate*. The first two are special data types, but the