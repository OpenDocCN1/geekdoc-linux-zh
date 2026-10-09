![](bbox=[0.0, 0.15, 1.0, 0.55])

**Figure 14.2**
Condor jobmonitor tool.

```
astro.cs.w   INTEL    LINUX    1.000    nice-user.condor@cs.chevre.cs.wisc.
aura.cs.wi   INTEL    LINUX    0.996    nice-user.condor@cs.chevre.cs.wisc.
balder.cs.   INTEL    LINUX    1.000    nice-user.condor@cs.chevre.cs.wisc.
bamba.cs.w   INTEL    LINUX    1.574    dmarino@cs.wisc.edu   riola.cs.wisc.e
bardolph.c   INTEL    LINUX    1.000    nice-user.condor@cs.chevre.cs.wisc.
...
```

**Removing a Job from the Queue.** You can remove a job from the queue at any time using the `condor_rm` command. If the job that is being removed is currently running, the job is killed without a checkpoint, and its queue entry is removed. The following example shows the queue of jobs before and after a job is removed.

`%  condor_q`