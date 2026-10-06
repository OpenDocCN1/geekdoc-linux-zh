# 24.4 Protocol Mechanisms for Data Exchange 503

tcp_cong_avoid(tp) implements the congestion growth within slow-start and congestion-avoidance algorithms. tcp_cong_avoid() is invoked when an incoming TCP segment with valid acknowledgement (ACK) is handled in tcp_ack(). (See Section 24.2.1).

Initially, the code checks for whether the TCP connection is still in the slow-start phase or is already in the congestion-avoidance phase:

The congestion window is increased by one in the slow-start phase (i.e., when the current value of the congestion window tp->snd_cnd is not bigger than the current threshold value tp->snd_sstresh). However, it must not exceed the upper limit value, tp->snd_cnd_clamp. This means that, in fact, the congestion window is increased by one upon each incoming acknowledgement. In practice, this means the amount of data that can doubles each time. This behavior corresponds to the exponential growth shown in Figure 24–16.

In the congestion-avoidance phase, the congestion window will be increased by one if n acknowledgments have been previously received, where n corresponds to the current congestion-window value.

To implement this behavior, the additional variable tp->snd_cnd_cnt is introduced; it is incremented by one upon each incoming acknowledgement (i.e., upon call of tcp_cong_avoid() in the congestion-avoidance phase). Next, when the congestion-window value tp->snd_cnd is reached, tp->snd_cnd can finally be increased by one, and tp->snd_cnd_cnt is reset. This method makes linear growth achievable.

In summary: there is initially an exponential increase of the congestion window, but, once the threshold has been reached, there is only a linear growth, as shown in Figure 24–16. Notice at this point that the congestion window increases continually in tcp_cong_avoid(). It increases until the criteria for a congestion are met, then it will cause it to reduce in the function described next.:

# tcp_enter_loss() net/ipv4/tcp_input.c

```
void tcp_enter_loss(struct sock *sk, int how)
{
    struct tcp_opt *tp = &sk->tp_info.of_tcp;
    (..)
    /* Reduce ssthresh if it has not yet been
       made inside this window. */
    if ((tp->ca_state <= TCP_CA_Disorder)
        || (tp->snd_una == tp->high_seq)
        || (tp->ca_state == TCP_CA_Loss && !tp->retransmissions))
    {
        tp->prior_ssthresh = tcp_current_sstresh(tp);
        tp->snd_sstresh = tp_recalc_sstresh(tp);
    }
}
```