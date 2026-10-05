# Transport 525

```
2598
2599    if(tp->num_sacks)
2600        tcp_sack_remove(tp);
2601
2602        tcp_fast_path_check(sk, tp);
2603
2604        if (eaten > 0) {
2605            _kfree_skb(skb);
2606        else if (!sk->dead)
2607            sk->data_ready(sk, 0);
2608            return;
2609        }
2610
2611 if (after(TCP_CB_CB(skb)->end_seq, tp->rcv_nxt))
2612     /* A retransmit, next most common case. Force an immediate ack. */
2613     NET_IN_STATS_BR(DelayedACKLost);
2614     tcp_enter_quickack_mode(tp);
2615     tcp_dsack_set(tp, TCP_CB_CB(skb)->end_seq, TCP_CB_CB(skb)->end_seq);
2616
2617 out_of_window:
2618     tcp_schedule_ack(tp);
2619 drop:
2620     _kfree_skb(skb);
2621     return;
2622 }
2623     
2624     /* Out of window. F.e. zero receive window probe. */
2625 if (!before(TCP_CB_CB(skb)->seq, tp->rcv_nxt+tcp_receive_window(tp)))
2626     goto out_of_window;
2627
2628     tcp_enter_quickack_mode(tp);
2629
2630 if (before(TCP_CB_CB(skb)->seq, tp->rcv_nxt)) {
2631         /* Partial packet, seq rcv_next < end_seq */
2632         SOCK_DEBUG(sk, "partial packet: rcv_next %X seq %X XX - %X\n",
2633             tp->rcv_nxt, TCP_CB_CB(skb)->seq);
2634 }
```

Figure 7.53 Processing and queuing incoming data (iii).

```
2634     TCP_CB_CB(skb)->end_seq);
2635
2636     tcp_dsack_set(tp, TCP_CB_CB(skb)->seq, tp->rcv_nxt);
2637
2638     /* If window is closed, drop tail of packet. After
2639         * remembering D-SACK for its head made in previous line.
2640         */
2641         if (!tp_receive_window(tp))
2642             goto out_of_window;
2643         goto queue_and_out;
2644     }
2645
2646     TCP_ECH_check_ca(tp, skb);
```