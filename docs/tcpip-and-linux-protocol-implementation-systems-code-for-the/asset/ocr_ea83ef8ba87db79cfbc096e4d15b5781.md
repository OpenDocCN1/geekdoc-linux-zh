# 776 TCP/IP and Linux Protocol Implementation

```
877      deficit = 0;
878
879      /* Start round */
880  do {
881      struct cbq_class *borrow = cl;
882
883
884
885      if (cl->q->q.qlen &&
886          (borrow == cbq_under_limit(cl)) == NULL)
887              goto skip_class;
888
889
890      if (cl->deficit <= 0) {
891              /* exhausted its allotment per
892              this round. Switch to the next one.
893              */
894              deficit = 1;
895              cl->deficit += cl->quantum;
896              goto next_class;
897      }
898
899
900
901  skb = cl->q->dequeue(cl->q);
```

# 9.175 CBQ-dequeue by priorities ii: linux/net/sched/sch_cbq.c.

```
898      /* Class did not give us any skb :-
899       It could occur even if cl->q->q.qlen != 0
900       f. e. if cl->q == "tbf"
901       */
902      if (skb == NULL)
903          goto skip_class;
904
905
906      cl->deficit -= skb->len;
907      q->tx_len = cl;
908      q->tx_borrowed = borrow;
909      if (borrow == 1) {
910          #ifndef CBQ_XSTATS_BORROWS_BYTES
911              borrow->xstats.borrows++;
912              cl->xstats.borrows++;
913          #endif
914      } else
915      else {
916
917          borrow->xstats.borrows += skb->len;
918          cl->xstats.borrows += skb->len;
919  #endif
920
921
922      q->tx_len = skb->len;
923
924      if (cl->deficit <= 0) {
925          q->active[prio] = cl;
926          cl = cl->next_alive;
927          cl->deficit += cl->quantum;
928      }
929
930      return skb;
```