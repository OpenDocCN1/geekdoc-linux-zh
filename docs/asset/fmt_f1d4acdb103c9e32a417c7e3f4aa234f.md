
```c
if (atomic_read(&sk)->rmem_alloc + skb) != sk->rcvbuf) {
    if (tcp_mem_schedule(sk, skb)) {
        if (tcp_prune_queue(sk) < 0 || tcp_mem_schedule(sk, skb)) {
            goto drop;
        }
    }
    /* Disable header prediction. */
    tp->pred_flags = 0;
    tcp_schedule_ack(sk);

    SOCK_DEBUG(sk, "out of order segment: rcv_next %x sock %x %X %XX\n",
        tp->rcv_nxt, TCP_SK_CB(skb)->seq, TCP_SK_CB(skb)->end_seq);

    tcp_set_owner(r, skb);

    if (skb_pkt(tp->out_of_order_queue) == NULL) {
        /* Initial out of order segment, build 1 ACK. */
        if (tp->p_ack(sk)) {
            tp->num_sacks = 1;
            tp->dsack = 0;
            tp->eff_acks = 1;
            tp->selective_acks[0].start_seq = TCP_SK_CB(skb)->seq;
            tp->selective_acks[0].end_seq = TCP_SK_CB(skb)->end_seq;
        }
        skb_queue_head(tp->out_of_order_queue, skb);
    } else {
        struct sk_buff *skb = tp->out_of_order_queue->prev;
        u32 seq = TCP_SK_CB(skb)->seq;
        u32 end_seq = TCP_SK_CB(skb)->end_seq;

        if (seq == TCP_SK_CB(skb)->end_seq) {
            __skb_append(skb, skb);
            if (tp->num_sacks == 0 ||
                tp->selective_acks[0].end_seq != seq)
                goto add_ack;
            /* Common case: data arrive in order after hole. */
            tp->selective_acks[0].end_seq = end_seq;
            return;
        }
    }
}
```

在 `tcp_rcv_established` 结束时，会调用 `tcp_data_queue`。这如图 7.51–7.54 所示。这里的路径是最常见的数据包处理，即按顺序且在当前窗口内。这里对拥有该套接字的当前任务进行了优化，否则必须保留内存并将套接字缓冲区队列。`rcv_nxt` 变量可以更新当前连接，如果套接字缓冲区包含某些数据，则调用 `tcp_event_data_rcv` 来调度一个 ACK。如果乱序队列中有数据包，则该段可能填充了空隙，在这种情况下应该立即调度一个 ACK。如果数据已经复制完成（即 `eaten > 0`），则最终可以释放套接字缓冲区；否则会调用 `sk->ready_data`，这将唤醒拥有套接字的任务。

次快的路径是接收重传的数据包，这会通知发送者然后将其丢弃。

下一次快的路径是零窗口探测。

该函数的剩余部分处理乱序到达的情况。

### 图 7.54 处理和入队输入数据 (iv)。

```c
2689    /* Find place to insert this segment. */
2690    do {
2691        if ((after(TCP_SKB_CB(skbi)->seq, seq)) {
2692                break;
2693            while ((skbi)->prev) != (struct sk_buff*)tp->out_of_order_queue) {
2694                /* Do sk overlap to previous one? */
2695                if (skbi && (struct sk_buff*)tp->out_of_order_queue &&
2696 before(seq, TCP_SKB_CB(skbi)->end_seq)) {
2697                    if (after(end_seq, TCP_SKB_CB(skbi)->end_seq)) {
2698                        /* All the bits are present. Drop. */
2699                        kfree_skb(skb);
2700                        tcp_dack_set(tp, seq, end_seq);
2701                        goto dack;
2702                    }
2703                } if (after(seq, TCP_SKB_CB(skbi)->seq)) {
2704                    /* Partial overlap. */
2705                    tcp_dack_set(tp, seq, TCP_SKB_CB(skbi)->end_seq);
2706                } else {
2707                    skbi = skbi->prev;
2708                }
2709            }
2710            skb_insert(skb, skbi->next, &tp->out_of_order_queue);
2711            /* And clear segments by new one. */
2712            while ((skbi = skbi->next) != NULL) && (struct sk_buff*)tp->out_of_order_queue &&
2713            after(end_seq, TCP_SKB_CB(skbi)->end_seq)) {
2714                if (before(end_seq, TCP_SKB_CB(skbi)->end_seq)) {
2715                    tcp_dack_extend(tp, TCP_SKB_CB(skbi)->end_seq);
2716                    break;
2717                }
2718            }
2719            skb_unlink(skbi, skbi->list);
2720            tcp_dack_extend(tp, TCP_SKB_CB(skbi)->end_seq);
2721            kfree_skb(skb);
2722        }
2723}
2724add_ack: {
2725    if (tp->sack_ok) {
2726        tcp_dack_new_skb(sk, seq, end_seq);
2727    }}
```

### 图 7.55 定器初始化。
