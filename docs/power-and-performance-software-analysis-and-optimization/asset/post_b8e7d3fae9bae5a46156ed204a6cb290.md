
# CHAPTER 6 Introduction to Profiling

## 6.2 TOP-DOWN HIERARCHICAL ANALYSIS

Top-Down Hierarchical analysis is a technique, developed by Intel, for using PMU events to decompose the flow of μops, in order to identify what pipeline stalls are affecting the overall pipeline efficiency. Each level within this hierarchy partitions the execution pipeline into a group of categories. Each category has zero or more subcategories, which increase the level of detail for further investigating the parent category. It is important to note that when the level of detail increases, moving to lower levels within the hierarchy, the level of error also increases. Intel provides a set of formulas that use the PMU events to calculate the percentage of μops attributed to each category. These formulas can be found in Figures 6.2–6.7.

This approach scales across multiple levels of granularity. For instance, this technique can be used over an entire application, by function, and so on.

Starting at the first level, that is, the top of the hierarchy, μops are divided into four distinct categories. These categories partition the execution pipeline based on the uop flow through a pipeline. A pipeline slot is an abstraction of the various resources, which again by microarchitecture, required for a uop to pass through the execution pipeline. The number of slots, also known as the width of the pipeline, controls the number of μops that can allocate and the number of μops that can retire in one clock cycle. At the time of writing, a width for

The Front End of the execution pipeline is responsible for fetching and decoding instructions from the instruction cache or memory. The act of delivering a uop from the Front End to the Back End, in order to begin execution, is referred to as allocation. Allocation marks the pipeline slots. As the uop in the Back End completes, its removal from the pipeline slot is referred to as retirement. Since one instruction can be comprised of multiple μops, an instruction isn't retired until all its μops have retired.

The four categories, at the very top of the Top-Down hierarchy, are organized based on whether a uop was allocated. If a uop was not allocated, there are two possible categories, which determine whether the Front End or Back End were responsible for the stall. The first category, Front Bound, corresponds to stalls during the instruction fetch and decode phases. In others, the Front End couldn't keep up with the Back End. The second category, Back Bound, corresponds to stalls where the fetch and decode occurred without incident, but the Back End was unable to accept the new uop. In other words, the Back End couldn't keep up with the incoming μops from the Front End.

On the other hand, if a uop was successfully allocated, the next question is whether uop retired, leading to two additional categories. The first category, Speculation, corresponds to the situation where a uop was successfully allocated but associated with a branch mispredict. As a result, a uop was removed from the pipeline without retiring. The second category, Retiring, corresponds to the ideal situation, where the uop is successfully allocated and then successfully retired.

Notice that three of the four categories, Bad Speculation, Front End Bound, and Back End Bound, sound fairly detrimental. Each of these categories represents stalls within the CPU pipeline, that is, unproductive cycles. Therefore, the percentage attributed to these categories are a less-is-better metric. On the other hand, the fourth category, Retiring, represents forward in the CPU pipeline, which is productive cycles. The percentage attributed to the Retiring is a higher-is-better metric.

The formulas for calculating the percentages attributed to each category are shown in Figure 6.2. The variables at the top of this figure, excluding W, are the PMU events required for the analysis. The IDQ_UOPS_NOT_DELIVERED is a nonarchitectural event introduced in the Second Generation Intel® Core™ processor family. As a result, this analysis requires a processor based on the Second Generation Intel microarchitecture or newer.

Since the width represents the number of μops that can be allocated per cycle, the denominator in each of these equations, the pipeline times the total number of cycles, represents the theoretical maximum of μops that could be allocated. Ideally, as shown in Equation 6.2(c), the number of retired μops would equal this theoretical maximum.

Once these metrics have been calculated, the next steps depend on which category dominates the results. Obviously, it is beneficial to first focus on the three categories that represent unproductive cycles. While a high retiring percentage indicates efficient pipeline utilization, it doesn't necessarily mean further performance can be obtained.

```
D = IDQ_UOPS_NOT_DELIVERED.CORE
M = INT_MISC_RECOVERY_CYCLES
N = CPU_CLK_UNHALTED_THREAD
R = UOPS_RETIRED_RETIRE_SLOTS
U = UOPS_ISSUED.ANY
W = pipeline width
```

| Metric | Formula | Reference |
| :--- | :--- | :--- |
| P_FE = % Front End Bound | (D/N) * 100 | (6.2a) |
| P_BS = % Bad Speculation | ((U - R + (W * M))/N) * 100 | (6.2b) |
| P_R = % Retiring | (R/N) * 100 | (6.2c) |
| P_BE = % Back End Bound | 100 - (P_BS + P_FE + P_R) | (6.2d) |

Figure 6.2: Equations for decomposing μops (Intel Corporation, 2014).

### 6.2.1 FRONT END BOUND

As mentioned, the Front End of the CPU pipeline is responsible for fetching instructions, decoding these into μops, and finally delivering these μops to the Back End. The general rule of thumb is to only focus on the Front End where the percentage is above 30% (Intel Corporation, 2014).

Instructions are fetched and decoded via the Legacy Decoder Pipeline, often referred to as the MITE. The MITE is responsible for fetching instructions from memory and decoding them into μops. These instruction fetches occur in 16-byte chunks. A dedicated cache, the ICache, and TLB, the ITLB, are used to reduce the overhead of memory accesses.

Once the instructions have been fetched, they are decoded by a series of decoding units. Each decoding unit is capable of generating a certain number of μops each cycle. In the case an instruction generates more μops than the decoding unit can handle, the instruction will require multiple cycles to decode. Once the instructions have been decoded, those μops are output to the μop queue. Starting with the Second Generation Intel microarchitecture, the μops will also be added to the Decoded ICache.

The Decoded ICache, often referred to as the DSB, caches the results of the Legacy Decoder Pipeline. This caching occurs in 32-byte chunks of instructions, which are indexed by the instruction pointer. There are various architectural restrictions on what instruction sequences can be cached. For example, on the Second Generation Intel microarchitecture, only two branches are allowed per entry and a maximum of 19 μops.

Before the MITE is invoked, the DSB is searched for the given instruction chunk, based on the address. If found within the cache, the fetch and decode phases are skipped, and the μops are delivered into the μop queue directly from the DSB. If not found, the MITE performs the decode, and then attempts to add all to the cache.

In the formula for Front End Bound, shown in Equation 6.2(a), the IDQ_UOPS_NOT_DELIVERED_CORE is compared against the theoretical maximum of μops. IDQ stands for the Instruction Decoder Queue, from where μops are allocated. In other words, this measures the number of times where μops was not delivered from the IDQ for allocation. As a result, the P_FE metric is the percentage of pipeline stalls caused by issues during the fetching or decoding of instructions.
