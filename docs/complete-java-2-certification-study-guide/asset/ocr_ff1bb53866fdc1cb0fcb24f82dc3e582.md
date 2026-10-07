# Monitors, Waiting, and Notifying 231

On line 5, the code calls notify() after changing the monitor's state. The notify() method arbitrarily selects one of the threads in the monitor's waiting pool and moves it to the Seeking lock state. Eventually, that thread will acquire the mailbox's lock and can proceed with execution.

Imagine a complete scenario. A thread could retrieveMessage() on a mailbox that has no message. It acquires the lock and begins the execution. It sees that the request flag is false, so it calls wait() and joins the mailbox's waiting pool. In this instance, no other thread is there in the pool. Because the producer calls storeMessage() and then notify(), it wakes up. Later, the producer calls storeMessage() on the same mailbox, the request flag is set to true. The producer then calls notify().

waiting pool: the consumer. So the consumer gets moved out of the waiting pool and into the Seeking lock state. Now the producer retrieveMessage(); because the producer has exited from synchronized code, it gives up the monitor's lock. The later consumer requires the lock and gets to execute: once this happens, it checks the request flag

sees a message in this scenario: a consumer tried to retrieve something, but there was nothing to consume, so the consumer waited. A producer later produced something, and at that point there was something for the consumer to consume, so the consumer notified; once the producer produced a message, the consumer consumed a message.

To briefly summarize this scenario: a consumer tried to consume something, but there was nothing to consume...

> As 7.7 shows, a waiting thread has ways to get out of the Waiting state that do not require a lock. One of the wait() calls takes an argument that specifies a lock timeout in milliseconds; if the timeout expires, no matter what version of wait() is invoked, if the waiting thread receives an interrupt() it moves immediately to the Seeking lock state.

This example protected the consumer against a wait() that retrieveMessage() and a notify() in storeMessage() might be empty. A prevention measure must be taken in the producer thread to prevent storeMessage() when the mailbox contains a message needs to wait and retrieveMessage() needs to notify. The mailbox class looks like this:

+   1. class Mailbox {
2. private boolean request;
3. private String message;
4. public synchronized void
5. storeMessage(String message) {
6. while(request == true) {