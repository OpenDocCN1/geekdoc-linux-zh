# Figure 7.39 Receiving a packet by the TCP layer (ii).

```
1647    ret = 0;
1648    if (!sk->lock_users) {
1649        if (tcp_prequeus(sk, skb))
1650            ret = tcp_v4_do_rcv(sk, skb);
1651    } else {
1652        sk_add_backlog(sk, skb);
1653        bb_unlock_sock(sk);
1654
1655\        sock_put(sk);
1656
1657    return ret;
1658
1659    no_tcp_socket:
1660    if (sk->len < (th->doff<<2) || tcp_checksum_complete(skb)) {
1661        bad_packet:
1662        TCP_INC_STATS_BH(TcpInErrs);
1663    } else {
1664        tcp_v4_send_reset(skb);
1665    }
1666    discard_it:
1667        /* Discard frame. */
1668        kfree_sk(skb);
1669        return 0;
1670    discard_and_release:
1671        sock_put(sk);
1672        goto discard_it;
1673    do_time_wait:
1674    if (sk->len < (th->doff<<2) || tcp_checksum_complete(skb)) {
1675        TCP_INC_STATS_BH(TcpInErrs);
1676        goto discard_and_release;
1677    }
1678    switch (sk->timwait_state_process((struct tcp_tw_bucket *)sk,
1679        sk, th, sk->len)) {
1680    case TCP_TW_SYN:
1681    {
1682        struct sock *sk2;
1683        sk2 = tcp_v4_lookup_listener(sk->nh->ip->addr,ntohs(th->dest),
1684        tcp_v4_ii(skb));
1685        if (sk2 != NULL) {
1686            tcp_tw_deschedule((struct tcp_tw_bucket *)sk);
1687            tcp_timwait_kill((struct tcp_tw_bucket *)sk);
1688            tcp_tw_put((struct tcp_tw_bucket *)sk);
1689        sk = sk2;
1690    }
1691    goto process;
1692}
1693    /* Fall through to ACK */
1694}
1695    case TCP_TW_ACK:
1696    tcp_v4_timwait_ack(sk, skb);
```