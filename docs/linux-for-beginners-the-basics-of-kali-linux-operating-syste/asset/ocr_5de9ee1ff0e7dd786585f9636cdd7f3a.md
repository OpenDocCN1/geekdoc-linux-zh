To use the critical section, we use the binary semaphore, as we did before. Let's call it to lock. It will be used by both the manufacturer and the consumer, protecting access to the buffer from other threads (again, both manufacturers and consumers)

+   2. In order to organize the manufacturer's expectations in the case of a full buffer, we will need a semaphore whose current value is equal to the number of free spaces in the buffer. Let's call it empty _items. The manufacturer, before attempting to add a new object to the buffer, reduces this semaphore to the standby state if it is equal to 0. The consumer, after removing the object from the buffer, will increase the semaphore by informing the manufacturers ( and waking up one of them)

+   3. In order to organize consumer expectations in the case of an empty buffer, a semaphore whose current value is equal to the number of seats in the buffer will be required. Let's call it full _ items. The consumer before attempting to pick up an object from the buffer reduces this semaphore, going into a state of waiting

Here is the pseudocode solution to this problem:

```
semaphore _t lock = 1; // for the critical section
  semaphore _t empty _ items = n; // 0 buffer full, empty from the beginning
  semaphore _t full_items = 0; // if 0 - the buffer is empty

// manufacturer
void producer ()
{
 item _t item = produce (); // create about ' object
  down ( empty _items); // is there a place for information ' facility ?
  down ( lock ); // enter the critical section
```