# Figure 7.65 Round-trip estimation (iii).

```
/* Calculate rto without বাচ্চ. This is the second half of Van Jacobson's
 * routine referred to above.
 * __inline__
 static __inline__ void tcp_set_rto(struct tcp_opt *tp)
{
     * Old crap is replaced with new one. 8
     * More seriously;
 * 1. If rto variance has been due to 50msec, it is hallucination.
 * It cannot be due to utterly erratic ACK generation made
 * at least by solaris and freed. "Erratic ACKs" has nothing,
 * to do with delayed acks, be at cvnd2 true timeout
 * is invisible. Actually, the round-trip linux-2.4 generates erratic
 * ACKs in some circumstances.
 */
tp->rto = (tp->rtt >> 3) + tp->rttvar;
/* 2. Lapse made earlier cannot be right.\ * If we do not estimate RTO correctly without them,
 * all the logic is pure shit and should be replaced
 * with correct one. It is exactly, we pretend to do.
 */
/* NOTE: clamping at TCP_RTO_MIN is not required, current algo
 * guarantees that rto is higher.
 */
 static __inline__ void tcp_bound_rto(struct tcp_opt *tp)
{
    if (tp->rto > TCP_RTO_MAX)
        tp->rto = TCP_RTO_MAX;
}
```

# Round-trip Estimation

In order to get more out of a TCP connection in terms of bandwidth utilization, an accurate method to determine the round-trip time for timeout purposes is needed. The mechanism is described in Stevens [8], and shown implemented in Figures 7.63-7.64.

# Figure 7.66 Building options on SYN packets.

```
/* Construct a tcp options header for a SYN or SYN_ACK packet.
 * If this is every changed make sure to change the definition of
 * MAX_SYN_SIZE to match the new maximum number of options that you
 * can generate.
 */
```