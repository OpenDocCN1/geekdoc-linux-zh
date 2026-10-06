# 380 Chapter 18 Using Traffic Control to Support Quality of Service (QoS)

To be able to store states between single transmit processes, the token-bucket-implementation uses the tbf_sched_data structure:

```
struct tbf_sched_data{
  u32 limit;               /*Maximal length of backlog: bytes*/
  u32 buffer;             /*Token Bucket depth/rate: Must Be >= MTU/B */
  u32 mtu;
  u32 max_size;
  struct qdisc_rate_table *R_tab;
  struct qdisc_rate_table *P_tab;
  /* Variables **/
  long tokens;            /*Current number of B tokens */
  long ptokens;           /*Current number of P tokens */
  psched_time_t t_c;      /*Time check-point */
  struct timer_list wd_timer; /*Watchdog timer */
};
```

The tbf limit field specifies the number of bytes in the queue used to buffer packets that cannot be sent immediately. The buffer field shows that the byte-to-rate (i.e. times) is used rather than bytes and rates for computations in most places within the implementation. This means that a packet with a specific length takes some transmit time from the bucket, the available time is calculated from the current number of tokens to the rate R ratio. The variables tokens and ptokens store the number of tokens in respect bucket. The time at which the last packet was transmitted to the t_c entry, and the wd_timer is needed when a timer has to be started for a packet's delayed transmission. Two pointers, R_tab and P_tab, point to the qdisc_rate_table, which stores the allocations of packet lengths to transmit times over divisions during each transmit process. This table is created by the function qdisc_get_rtabb(*rtabb) with tbf_change(net/sch_tbf.c) initializes the token-bucket filter. However, the actual computation is done in the user space by use of the tc_calc_rtab() function in iproute2/tc_core.c.

We will now introduce and explain additional functions of the token-buffer filter:

```
tbf_init()
```

Initialization of the token buffer means that the start time has to be initialize the timer. The macro PSCHED_GET_TIME(include/net/sched.h) is used to establish the start time. This macro accesses the TSC register described in Chapter 2, if it is present. A structure containing to private data and a pointer to the tbf_watchdog() function are passed to the timer. The tbf_watchdog() function has to be invoked when the timer expires.

```
tbf_enqueue()
```

This function serves to accept packets and append them to the end of the queue. Also, a number of statistics are updated, and error cases are handled.