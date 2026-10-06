# 8.1 Event infrastructure 157

SAMPLE 0x400c4c

```
16 Branches in Stack
From: 400c4c : mispredicted
From: 400c62 : predicted
From: 400c52 : predicted
From: 400c62 : predicted
From: 400c4c : predicted
From: 400c62 : predicted
From: 400c52 : predicted
From: 400c62 : predicted
From: 400c4c : mispredicted
From: 400c62 : predicted
From: 400c52 : predicted
From: 400c62 : predicted
From: 400c4c : mispredicted
From: 400c62 : predicted
From: 400c52 : predicted
From: 400c62 : predicted
```

SAMPLE 0x400710

```
16 Branches in Stack
From: 400710 : mispredicted
From: 400c78 : predicted
From: 400c52 : predicted
From: 400c62 : predicted
From: 400c4c : predicted
From: 400c62 : predicted
From: 400c52 : predicted
From: 400c62 : predicted
From: 400c4c : predicted
From: 400c62 : predicted
From: 400c52 : predicted
From: 400c62 : predicted
From: 400c4c : predicted
From: 400c62 : predicted
From: 400c52 : predicted
From: 400c62 : predicted
```

Looking at these results, a couple of different branches are highlighted. The results seem to corroborate the earlier hypothesis that the branch predictor was
adept at predicting the microbenchmark workload. The branches with an instruction
point around 0x400000 are clearly the user application's branches, which addresses such as 0xffffff812e are clearly branches in kernel code. Notice that
on line 97 of Listing 8.3, perf_attr.exclude_kernel is set. As a result, even if one
of the kernel branches was mispredicted, it would not appear in the sample data. At
the time, the LBR records all branches, which is why both user and kernel space
addresses appear in the branch stack.