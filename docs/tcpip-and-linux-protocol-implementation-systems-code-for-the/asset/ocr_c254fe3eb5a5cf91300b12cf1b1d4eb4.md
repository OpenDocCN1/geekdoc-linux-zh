# 658 TCP/IP and Linux Protocol Implementation

There are a number of scheduling dimensions:

**Priority levels.** If we implement a priority system, how many levels should be there? It is not obvious why you want more than two or three. Since a higher-priority queues services first, this approach can cause starvation for lower-priority queues, unless we have some sort of admission control for the overall occupancy of the higher-priority service in the network, or on any given path.

**Work-conserving or not.** We must decide if delay/jitter control is required. Is the cost of implementation of delay/jitter control in a network acceptable? In practice it isn't.

**Degree of aggregation.** What is the flow granularity? Do we have per-application flow, or per-user or per-end system? It is a question of tradeoff the cost of implementation of the scheduling system (in terms of state, state setup messages, classification frequency, and complexity) and the granularity of control.

**Servicing within a queue.** Can we get away with FCFS within a queue? Should we check for other parameters? What other added processing overhead may be there (e.g., network management/logging). What kind of queue management do we need in an emergency?

# 9.6.1 Common Scheduling Disciplines

Let's now look at some of the more common systems for picking which to send next, and when to send it.

**Priority queuing.** We have $K$ queues: $1 <= k <= K$. Queue $k + 1$ has greater priority than queue $k$. In other ways, higher-priority queues are serviced first. This is very simple to implement and has a low processing overhead. It offers fairly relative priority in practice (assuming we keep no history), and this offers no deterministic performance bounds. In terms of fairness and protection, it is not max-min fair and it hazards the risk of starvation of lower-priority queues.

**Generalized processor sharing (GPS).** This is a work-conserving scheme, and it serves an infinitesimally small amount of data from flow $i$ and then visits the next flows round robin. This provides a max-min fair share to each flow. However in practice it is not directly implementable. Instead, it is used as a baseline abstract reference for comparing other schedulers.

**Weighted round robin.** This is the simplest attempt at an implementable approximation of GPS. The queues are visited round robin in proportion to weights assigned. Since different flows have different mean packet