If the current version of Pthreads mutexes does not meet all your needs, you could build your own extensions on top of them.

# # Deadlock Prevention

Imagine two toddlers playing with some toys. One child sees what the other child is playing with and vice versa. They want each other's toys, but they are not willing to give up what they have. Essentially, they are deadlocked.

When using threads, be sure to consider the possibility of resource contention and critical sections. After isolating and grouping the critical data, you need to identify who needs what and when. Sometimes you may find that two resources need to be locked (called *interlocked*) before work can proceed. If you are not careful, you can cause a deadlock to occur.

Consider the following deadlock example:

| Thread #1 | Thread #2 |
| --- | --- |
| 1. Lock Savings Fund. | 1. Lock IRA Fund. |
| 2. Lock IRA Fund. | 2. Lock Savings Fund. |
| 3. Using IRA Fund, change Savings Fund. | 3. Using Savings Fund, change IRA Fund. |
| 4. Unlock IRA Fund. | 4. Unlock IRA Fund. |
| 5. Unlock Savings Fund. | 5. Unlock Savings Fund. |

Thread #2 deadlocks at step 2. Using a standardized naming policy, the deadlock is more apparent:

| Thread #1 | Thread #2 |
| --- | --- |
| 1. Lock `Funds_Mutex_1`. | 1. Lock `Funds_Mutex_2`. |
| 2. Lock `Funds_Mutex_2`. | 2. Lock `Funds_Mutex_1`. |
| 3. **Using** `Funds_Mutex_2`, | 3. **Using** `Funds_Mutex_1`, **change** `Funds_Mutex_1`. |
| 4. Unlock `Funds_Mutex_2`. | 4. Unlock `Funds_Mutex_2`. |
| 5. Unlock `Funds_Mutex_1`. | 5. Unlock `Funds_Mutex_1`. |

The deadlock occurs because the two threads want each other's resources. The following are a few rules that can reduce deadlock potential:

+   * Group Naming—Identify interdependent groups of resources and give their mutexes a similar name (for example: `Funds_Mutex_1` and `Funds_Mutex_2`).
* In-Order Locking—Lock the resources numerically from least to greatest.
* In-Order Unlocking—Unlock the resources numerically from greatest to least.

By following these deadlock policies, you can avoid the nasty debugging required in unraveling a deadlock.

# # Controlling Children and Killing Zombies

You have created a couple of threads or processes. After you have created children, you do have some control over them. The question is, how do you control their behavior? As mentioned before, you can communicate with them using signals, messages, and data.