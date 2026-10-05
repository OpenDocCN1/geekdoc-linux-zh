# Figure 7.25 Start of tcp_sendmsg.

```
1008 int tcp_sendmsg(struct sock *sk, struct msghdr *msg, int size)
1009 {
1010     struct iovec *iov;
1011     struct tcp_opt *tp;
1012     struct sk_buff *skb;
1013     int iovlen, flags;
1014     int mss_now;
1015     int err, copied;
1016     long timeout;
1017
1018     tp = &(sk->tp->pinfo.af_tcp);
1019
1020     lock_sock(sk);
1021     TCP_CHECK_TIMER(sk);
1022
1023     flags = msg->msg_flags;
1024     time = sock_mdtime(sk, flags&MSG_DONTWAIT);
1025
1026     /* Wait for a connection to finish. */
1027     if ((i << sk->state) & (TCPCF_ESTABLISHED | TCPF_CLOSE_WAIT))\n1028         if ((err = wait_for_tcp_connect(sk, flags, &timeout)) != 0)
1029             goto out_err;
1030
1031     /* This should be in poll */
1032     clear_bit(SOCK_ASYNC_NOSIGNACE, sk->socket->flags);
1033
1034     mss_now = tcp_current_mss(sk);
1035
1036     /* Ok commence sending. */
1037     iovlen = msg->msg_iovlen;
1038     iov = msg->msg_iovlen;
1039     copied = 0;
1040
1041     err = -EPIPE;
1042     if (err = errerr || (sk->shutdown&SEND_SHUTDOWN))\n1043         goto do_error;
```

# Figure 7.26 Determine MSS.

```
892 /* Compute the current effective MSS, taking SACKS and IP options,
893  * and even PMTU discovery events into account.
894  */
895
896 static __inline__ unsigned int tcp_current_mss(struct sock *sk)
897 {
898     struct tcp_opt *tp = &(sk->tp->pinfo.af_tcp);
899     struct dst_entry *dst = &sk_dst_get(sk);
900     int mss_now = tp->mss_caches;
901
```