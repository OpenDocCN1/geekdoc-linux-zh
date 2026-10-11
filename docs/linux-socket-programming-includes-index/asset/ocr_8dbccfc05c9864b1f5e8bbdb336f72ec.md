# **PART II**

This chapter introduced you to the topic of multitasking and the different types of tasks—
processes and threads. You also learned how to create them with high-level tools like **Pthreads**
or *fork()* or the low-level tool __clone().

After you have created the task, you can control thread interactions with synchronization.
Synchronization further helps you serialize (or coordinate) access to the contended data.
Serialization ensures data integrity.

Every task can accept messages through pipes or other I/O and signals to handle asynchronous
events. The pipes allow you to direct information to children, offloading the parent. They also
allow you to redirect standard I/O for simpler interaction. Signals capture events that can help
your programs be more robust.

The next chapter extends the concepts of I/O and provides alternatives to multitasking.