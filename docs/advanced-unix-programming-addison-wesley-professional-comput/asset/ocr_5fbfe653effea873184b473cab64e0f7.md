This works OK, but Thread B wastes a lot of CPU time when the queue is empty, as it keeps checking while it loops and loops. You could slow it down a bit this:

+   Thread A
+   1. Read data [B]
+   2. Lock M [b]
+   3. Put item on queue
+   4. Unlock M
+   5. Goto step 1
+   
+   Thread B
+   1. Lock M
+   2. If item on queue, remove it and update database
+   3. Unlock M [b]
+   4. Sleep for 1 sec. [b]
+   5. Goto step 1

But this isn’t much of an improvement: Thread B is now less responsive because it may be sleeping when there’s work to do, and it still wastes CPU time because the queue may be empty when it wakes up. What we want to do is have Thread A signal Thread B when it puts an item on the queue and have Thread B block until it gets the signal. Let’s try it with another mutex $Q$ to represent the concept “$Q$*queue is nonempty*”:

+   Thread A
+   1. Read data [B]
+   2. Lock M [b]
+   3. Put item on queue
+   4. Unlock M
+   5. Unlock $Q$
+   6. Goto step 1
+   
+   Thread B
+   1. Lock M [b]
+   2. If item on queue, remove it and update database
+   3. Unlock M
+   4. Lock $Q$ [B]
+   5. Goto step 1

Thread B’s attempt to lock $Q$ (step 4) is an indeterminate block because $Q$ becomes unlocked only when Thread A returns from its read (step 1).

Now the problem is that Thread A may try to unlock $Q$ when Thread B hasn’t got it locked, which would be a lost signal—the attempt to unlock isn’t somehow remembered for the next attempt to lock (i.e., mutexes are not counting semaphores). So if this happens, Thread B will be held up waiting for the lock on $Q$, and the lock won’t be released until the next time data is read, if ever. Meanwhile, the item on the queue goes unprocessed by Thread B.

A more concrete problem with $Q$ is that only the thread that locks a mutex can unlock it. So, A’s step 5 would result in an error.