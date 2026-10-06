# 18.4 Kernel Structures and Interfaces 375

change() include/net/pkt_sched.h

The change() function is used to change class parameters or create new classes, provided that the queuing discipline allows this.

delete() include/net/pkt_sched.h

This function checks on whether the class is still referenced, and it deletes the class if this holds true.

walk() include/net/pkt_sched.h

This function walks through the linked list of all the classes of a queuing discipline, and invokes a callback function to fetch configuration data and statistical parameters.

tcf_chain() include/net/pkt_sched.h

Figure 18–2 shows that each class is bound to at least one filter. The function tcf_chain() returns a pointer to the beginning of a linked list for the filter bound to that class.

bind_tcf() include/net/pkt_sched.h

This function tells the queuing discipline that a filter is going to be bound to the class. This means that the function is similar to the get() function, but can be used in some cases where we have to run additional checks.

unbind_tcf() include/net/pkt_sched.h

This function is the counterpart of the previous function, bind_tcf(), which means that it represents an extension of the put() function.

dump_class() include/net/pkt_sched.h

The dump() function for queuing disciplines, the function dump_class() serves to output configuration parameters and statistical data for a class.

# 18.4.4 Filters

The class packets that passed by the enqueue() function in a queuing discipline belong to is decided by filters.