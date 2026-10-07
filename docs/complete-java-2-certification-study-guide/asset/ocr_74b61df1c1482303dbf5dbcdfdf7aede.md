# Controlling Threads

Thread control is the art of moving threads from state to state. You control threads by triggering state transitions. This section examines the various pathways out of the Running state. These pathways are

+   - Yielding
- Suspending and then resuming
- Sleeping and then waking up
- Blocking and then continuing
- Waiting and then being notified

The first four of these pathways are presented below. The fifth concerns monitors, and is discussed in the major section "Monitors, Waiting, and Notifying."

# Yielding

A thread can offer out to the virtual CPU by yielding. A call to the yield() method causes the currently executing thread to move to the Ready state if the scheduler is willing to run any other thread in place of the yielding thread. The Yield state is shown in Figure 7.2.

A thread that has yielded goes into the Ready state. There are two possible scenarios. If any other threads are in the Ready state, then the thread that just yielded might have to wait a before it gets to execute again. However, if no other threads are waiting, then the thread that yielded will get to continue executing immediately. Note that most schedulers do not stop the thread from running in favor of a thread of lower priority.

The yield() method is a static method of the Thread class. It always causes the currently executing thread to yield.

FIGURE 7.2 Yield

![](bbox=[0.253, 0.696, 0.417, 0.903])