# TABLE 7.1 The Function of Each Parameter for the pthread_create() Library Call

| Parameter | Description |
|---|---|
| child | The handle to the new thread. You use this variable after the call to control the thread. |
| attr | A set of attributes or behaviors for the new thread. You can define how the thread is to work and interact with the parent at the time of instantiation. A few of these behaviors include priority, attachment, and scheduling. This parameter can be NULL. |
| fn | A pointer to a function that is to house the thread. Every thread runs in a specified program subroutine (unlike fork()). When the thread returns or exits the subroutine, the system terminates the thread. This helps avoid the task confluence problem (see above). |
| arg | A parameter to be passed to the function. You can use this to configure the thread's initial settings. Be sure to make the data block that this parameter points to available to the thread. In other words, don't refer to a stack variable. The parameter can be NULL as well. |

As previously noted, you have two threads running after successfully completing the call—the parent and the child. Both share everything except the stack. The parent keeps a handle (*child*) of the child thread, and the child executes in own routine (*fn*) with configuration (*arg*) and behavior (*attr*). If you set the attributes to NULL, you can still change the thread's behavior later. Keep in mind that until you change the attributes, the thread behaves in the default manner.

Essentially, the call reduces to two specific parameters. You can compare the basic algorithms for processes and threads in the following code. The algorithms almost mirror each other to reflect the primary differences. Compare Listings 7.4 and 7.5 to see the differences in creating processes and threads.

# LISTING 7.4 Process Creation Examples

```
```/* This example creates a process */
void Child_Fn(void)
{
```