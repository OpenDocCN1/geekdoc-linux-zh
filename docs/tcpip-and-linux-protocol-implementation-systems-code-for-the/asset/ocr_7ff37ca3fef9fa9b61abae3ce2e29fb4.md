# 534 TCP/IP and Linux Protocol Implementation

# Figure 7.63 Round-trip estimation (i).

+   * Called to compute a smoothed rtt estimate. The data feed to this
* routine either from timestamps, or from segments that were
* known_not_ to have been retransmitted [see Karn/Partridge
* Proccessings SIGCOMM 87. The algorithm is from the SIGCOMM 88
* piece by Van Jacobson
* NOTE: the next three routines used to be one big routine.
* the cycle in the RFC 123 implementation it was better to break
* it up into three procedures. - erics
*/

```
static __inline__ void tcp_rtt_estimator(struct tcp_opt *tp, __u32 mrtt)
    long m = rtt; // rtt */
```

> /* The following awesome comes from Jacobson's
article in SIGCOMM '88. Note that rtt and mdev
are are scaled versions of rtt and mean deviation.
This is designed to be as fast as possible
m stands for "measurement".
On a 1990 paper the rto value is changed to:
RTO = rtt + 4 * mdev
* Funny. This algorithm seems to be very broken.
This formula estimates RTO, when it is decreased, increase
too slowly, when it is increased fastly, decrease too fast
etc. I guess in BSD RTO takes ONE value, so that it is absolutely
does not matter how to _calculate_it. Seems, it was trap
that VJ failed to avoid. 8)
*/

When a SACK option comes in, the relevant socket buffer is marked as
received and not retransmitted. A receiver still has the option to drop the packet
(act known as reneging) (see Figure 7.61).

# Figure 7.64 Round-trip estimation (ii).

```
if (m == 0)
    m = 1;
if (tp->rtt != 0) { /* m is now error in rtt est * */
    m = (tp->rtt >> 3); /* rtt = 7/8 + 1/8 new * */
    tp->rtt += m;
if (m < 0) {
    m = -m;
    m = (tp->mdev >> 2); /* similar update on mdev */
    * This is similar to one of Eifel's findings.
* Eifel blocks blocks mdev updates when rtt decreases.
* This solution is a bit different: we use finer gain
* for mdev in this case (alpha+beta).
* Like Eifel it prevents growth of rto,
```