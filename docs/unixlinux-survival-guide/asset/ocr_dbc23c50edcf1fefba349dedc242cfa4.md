# 3.1 WHAT IS BASELINING?

Baselining is the process of sampling a variety of counters the system provides. The name stems from the idea that the samples taken during normal operation provide a base to decide if something might be wrong with the machine. Sampling this type of data should start right after the machine is set up and continue during the lifespan of the system.

# 3.1.1 Why Baselining?

There are many advantages to taking constant measurements of a productive system. Naturally, the most obvious is the fact that a deviation of one or more values from the "norm" points to a possible issue with the machine. Baselining provides the system administrator with the necessary foundation to discover the deviation in the first place. Every system tends to change over time, with higher workloads, more users, etc. If a solid foundation of baselines exists, the one in charge of keeping the system up and running (you) will be able to determine if the machine is just "loaded", if the machine needs a hardware upgrade, for example, another CPU or more RAM; or if the system shows any erratic behavior that needs to be taken care of. Using the data over time even yields a good base to convince the person(s) in charge of the IT budget that the time has come to invest money in the system(s) to keep up with user demands or increased workloads.

Also, a nice side effect is that the system administrator is able to figure out if the system is really "slow" or if the user complaining about the "slowness" of the machine is simply under pressure to finish some work in time. In the latter case, try to find out how to help the user and rest assured the machine is doing what it is supposed to be doing right now.

One last thing to cover before we dive into the work: even if the sampling of the data imposes a slight performance hit on the system, you should try to generate the logs and graphs every time a sample is generated. If the machine should crash, it might still be possible to recover this data and get a clue what happened.

# 3.1.2 What to Baseline

Some people consider making the decision as to what needs to be baselined a "black art," information passed on by the ones in the know during strange rituals or by pure coincidence. The fact is that, depending on the tasks that a system needs to fulfill to justify its existence, the data that should be sampled in any given situation differs greatly. Some counters are needed for every computer; others are related to a special purpose or a certain business case. The values to be monitored discussed in the following sections are of general nature; this means they should be monitored regardless of the system's purpose.