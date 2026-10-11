# Load Balancing

The scheduler attempts to keep the system load as balanced as possible. It does this by running rebalance code when tasks change state or make specific system calls, called event balancing, and at specified intervals measure in jiffies, called active balancing. Tasks must do something explicit for event balancing to take place, whereas active balancing occurs without any action from any task.

Event balance policy is defined in each sched domain data structure, again depending on the system topology.

When an event balancing occurs, the scheduler searches up the domain hierarchy and performs the load balancing at the highest domain that suggests a load balancing.

Active balancing happens at each tick. The scheduler starts at the lowest domain and works its way up, checking the last time the domain is balanced and the interval the domain specified for rebalancing. This is to determine if the domain should be balanced. The scheduler does balancing, if warranted.

When a run queue of a processor becomes empty, it proactively pulls tasks from other run queues to balance the load.

In addition to keeping the system load balanced, the scheduler also has tunable parameters that can improve response time for those critical tasks.