the mailbox object is ready to handle another request.) It is tempting to implement the
thread like this:

+   1. public class Consumer extends Thread {
2. private Mailbox myMailbox;
3.
4. public Consumer(Mailbox box) {
5. this.myMailbox = box;
6. }
7.
8. public void run() {
9. while (true) {
10. if (myMailbox.request) {
11. System.out.println(myMailbox.message);
12. myMailbox.request = false;
13. }
14.
15. try {
16. sleep(50);
17. }
18. catch (InterruptedException e) { }
19. }
20. }

The consumer thread loops forever, checking for requests every 50 millisecond. If there is
a request (line 10), the consumer thread writes the message to standard output (line 11) and then
sets request to false that it is ready for more requests.\ Consumer class may look fine at glance, but it has two serious problems:

+   * The Consumer accesses data internal to the Mailbox class, introducing the possibility
of corruption. On a time-sliced system, the consumer thread could just possibly be inter-
rupted between lines 10 and 11. The interrupting thread could possibly be a client that
sets message to its own (ignoring the convention of checking request to see if the
hler is available). The consumer would send the wrong message.
* The choice of 50 milliseconds for the delay can never be ideal. Sometimes 50 milliseconds
be too long, and clients receive slow service; sometimes 50 milliseconds will be too
frequent, and cycles will be wasted. A thread that wants to send a message has a similar
dilemma if it finds the request flag set: the thread should back off for a while, but for how
long? There is no good answer to this question.\ Ideally, these problems would be solved by making some modifications to the Mailbox class:
* The mailbox should be able to protect its data from irresponsible clients.