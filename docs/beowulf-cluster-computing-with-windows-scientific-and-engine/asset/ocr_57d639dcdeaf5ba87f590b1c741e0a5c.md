it supports interactive jobs (described next) and a user cannot easily gauge CPU time while running interactively but can watch the clock on the wall to know when their time allocation will end.

+   • `rem ccs type:` Cluster CoNTroller supports both batch and interactive jobs. If you request a batch job (e.g., `rem ccs type = batch`), the scheduler will run your batch file for you, as you on the master node, or the first node in the set you are allocated. Anything in the batch file you submitted will be run on the master node. This allows you to submit work to the system to be done later, for example over a weekend. If you prefer to log in to the nodes you are allocated and run your jobs by hand (debugging work, for example), you can request interactive time (e.g., `rem ccs type = interactive`). For interactive jobs Cluster CoNTroller gives you access to the nodes and then gets out of the way. When the type you requested is up, Cluster CoNTroller will kill your processes (including Telnet sessions to the nodes) and make the resources available for the next job.

In addition to these four requirements, there is an optional field:

+   • `rem ccs requirements` Cluster CoNTroller supports heterogeneous resource scheduling. Hence, if you have multiple types of node resources, you can specifically request them. The `cctypes` command will show you the various types of node resources your cluster has available. Note that if all your nodes are the same, this keyword is not necessary. An example would be `rem ccs requirements = @development.` This is interpreted as 8 nodes that have a feature named “development.”

All Cluster CoNTroller commands are prefaced in a Windows batch file (.bat extension) with `rem ccs`. These lines are parsed and checked when a user submits a job.

**JobSetup.** The last item in your batch file, following the Cluster CoNTroller directives, is the actual work you want done in batch. Interactive jobs read the Cluster CoNTroller directives to allocate the necessary resources. The batch file is not started on the nodes. Batch jobs actually this batch file on the master node. The example in Figure 17.5 illustrates a batch file that runs a “Hello World” program over two different network interfaces, one after the other.

Let’s go through this example line by line. The commands

```
```
set MPI_COMM=TCP
```

```

and