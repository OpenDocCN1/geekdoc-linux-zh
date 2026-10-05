# Figure 7.57 Recording the next selectively acknowledge an out-of-order segment (i).

```
2397 static void tcp_sack_new_of_skb(struct sock *sk, u32 seq, u32 end_seq)
2398 {\n2399     struct tcp_opt *tp = &sk->tp->pinfo.af;
2400     struct tcp_sack_block *block = &tp->selective_acks[0];
2401     int cur_sacks = tp->num_sacks;
2402     int this_sacks;
2403 
2404     if (cur_sacks) {
2405         goto new_sack;
2406 
2407         for (this_sack=0; this_sack<cur_sacks, sp++) {
2408             if (tcp_sack_extend(sp, seq, end_seq)) {
2409                 /* Rotate this sack to the first one. */
2410                 for (:; this_sack>0; this_sack--, sp--) {
2411                     tcp_sack_swap(sp, sp-1);
2412                 if (cur_sacks > 1)
2413                     tcp_sack_maybe_coalesce(tp);
2414                 return;
2415             }
2416             }
2417             /* Could not find an adjacent existing SACK, build a new one,\n2418                 * put it at the front, and shift everyone else down. We
2419                 * always know there is at least one SACK present already here.
2420             */
2421             * If the sack array is full, forget about the last one.
2422             */
2423             if (this_sack > 4) {
2424                 this_sack--;
2425                 tp->num_sacks--;
2426                 sp--;
2427             }
2428             for(;this_sack > 0; this_sack--, sp--) {
2429                 *sp = *(sp-1);
2430             }
2431     new_sack:
2432             /* Build the new head SACK, and we're done. */
2433             sp->start_seq = seq;
2434             sp->end_seq = end_seq;
2435             tp->num_sacks++;
2436             tp->eff_sacks = min(tp->num_sacks+tp->dsack, 4-tp->tstamp_ok);
2437         }
2438 
2439 static __inline_int(struct tcp_sack_block *sp, u32 seq, u32 end_seq)
2440 {
2441     if (!after(seq, sp->end_seq) && \& !after(sp->start_seq, end_seq)) {
2442         if (before(seq, sp->start_seq)) {
2443             sp->start_seq = seq;
2444         } if (after(end_seq, sp->end_seq)) {
2445             sp->end_seq = end_seq;
2446         return 1;
2447     }
2448     return 0;
2449 }
```