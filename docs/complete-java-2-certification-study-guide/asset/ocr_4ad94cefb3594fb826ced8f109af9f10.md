# Chapter 7 · Threads

**Both wait() and notify() must be called in synchronized code** A thread that calls wait() releases the CPU; at the same time, it releases the lock. it enters a pool of waiting threads, which is managed by the object whose wait() method called. Every object has such a pool.

The following code shows the Mailbox class's retrieveMessage() method could be modified to begin taking advantage of calling wait():

+   1. public synchronized retrieveMessage() {
2. while (request == false) {
3. try {
4. wait();
5. catch (InterruptedException e) { 
6. }
7. request = false;
8. return message;
9. }

Now consider what happens when a message-consuming thread calls this method. The call might look like:
MailBox.retrieveMessage();

When a message-consuming thread calls this method, the thread must first acquire the lock for myMailbox. Acquiring the lock could happen immediately, or it could incur a delay if some other thread is executing any of the synchronized code of myMailbox. One way the first code checks the request consumer thread has the lock and begins to execute at line 2. If the flag is not set, then myMailbox has no message for the thread. In this case the wait() method is called at line 4 (it can throw an InterruptedException, so the try/catch code is required, and while will reset the condition). When line 4 executes, the consumer thread ceases execution; it releases the lock for myMailbox and enters the pool of waiting.
The consumer has been successfully prevented from corrupting the Mailbox monitor.
Unfortunately, it is stuck in the monitor's pool of waiting threads. When the monitor changes to a state where it can provide the consumer with something to do, then something will have to get the consumer out of the Waiting state. This is done by calling notify() when the monitor's request flag becomes true, which happens only in the storeMessage() method. The revised storeMessage() looks like:

+   1. public synchronized void
2. storeMessage(String message) {
3. this.message = message;
4. request = true;
5. notify();
6. }