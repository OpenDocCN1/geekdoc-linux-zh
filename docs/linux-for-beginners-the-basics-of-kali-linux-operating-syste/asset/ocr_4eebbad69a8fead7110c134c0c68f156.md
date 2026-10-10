must write the code so that at the stage of development, there is room for errors. Let us familiarize ourselves with the rules that must be followed in order for the generated code to comply with this principle. Consider the main approaches to competition problems.

Sometimes (but rarely enough) you can just ignore these mistakes. This may make sense when we are not interested in the accurate recording of particular data, but collect statistics about them, so individual errors will not affect the overall result. For example, a global counter is a value on which to calculate the average number of requests to the system per day, and you can ignore the error of registering such requests that occur every few hours. Unfortunately, in most cases, this approach is not accepted.

Sometimes, the use of global data is not dictated by the specifics of the task. In this case, the straightforward solution is to create local copies of data for each stream and operate them only. In practice, this works very well and should be used wherever possible. For example, if the specifics of the problem allow the creation of a separate counter for each thread (or global array of counters, where each element is changed only by a certain flow), the implementation of such data structures solves the problem. Again, such a solution cannot be applied in all cases (for example, in the situation with bank accounts, different flows, after all, must somehow modify the total for all accounts).

In all other cases, changes must be protected against the effects of other flows. This is the main task of synchronization. Consider different approaches to solving it.

# Critical Sections And Locks

# The Concept Of Critical Section

Consider using a simpler idea to solve a competition problem. It is easy to see how the source of our mistake is that, from the outside, the simplest money-transferring operation actually breaks down into several operations, with the chance of any other flow interfering