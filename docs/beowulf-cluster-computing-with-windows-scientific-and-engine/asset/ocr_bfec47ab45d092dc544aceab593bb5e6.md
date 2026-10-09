**The Lifespan of a Job Executing in Condor.** When a job is submitted to Condor, the `condor_negotiator` performs matchmaking to find a suitable resource to use for the computation. This process involves satisfying both the job and the machine’s requirements for each other. The machine can define the exact conditions under which it is willing to be considered available for running jobs. The job can define exactly what kind of machine it is willing to use.

Once a job has been matched with a given machine, there are four states the job can be in: running, suspended, graceful shutdown, and quick shutdown. As soon as the match is made, the job sets up its execution environment and begins running.

While it is executing, a job can be suspended (for example, because of other activity on the machine where it is running). Once it has been suspended, the job can resume execution or can move on to preemption or eviction.

All Condor jobs have two methods for preemption: graceful and quick. Graceful implies that the program told to get off the system, but it is given time to clean up after itself. A quick shutdown involves rapidly killing all processes associated with a job, without giving them any time to execute their own cleanup procedures. The Condor system performs checks to ensure that processes are not left behind once a job is evicted from a given node.

**Condor Policy Expressions.** Various expressions are used to control the policy for starting, suspending, resuming, and preempting jobs.

+   START: when the `condor_startd` is willing to start executing a job.
+   
+   RANK: how much the `condor_startd` prefers each type of job running on it. The `RANK` expression is a floating-point instead of a Boolean value. The `condor_startd` will preempt the job it is currently running if there is another job in the system that yields a higher value for this expression.
+   
+   WANT_SUSPEND: controls whether the `condor_startd` should even consider suspending this job or not. In effect, it determines which expression, `SUSPEND` or `PREEMPT`, should be evaluated while the job is running. `WANT_SUSPEND` does not control when the job is actually suspended; for that purpose, you should use the `SUSPEND` expression.
+   
+   SUSPEND: when the `condor_startd` should suspend the currently running job. If `WANT_SUSPEND` evaluates to `TRUE`, `SUSPEND` is periodically evaluated whenever a job is executing on a machine. If `SUSPEND` becomes `TRUE`, the job will be suspended.
+   
+   CONTINUE: if and when the `condor_startd` should resume a suspended job. The `CONTINUE` expression is evaluated only while a job is suspended. If it evaluates