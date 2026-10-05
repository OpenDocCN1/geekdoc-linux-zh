# 798 TCP/IP and Linux Protocol Implementation

```
164      add_timer(&elist[est->interval].timer);
165  }
166      write_lock_bb(&est_lock);
167      elist[est->interval].list = est;
168      write_unlock_bb(&est_lock);
169      return 0;
170  }
```

**Figure 9.216** Rate estimator–estimation timer routine for estimation: linux/net/scheduler.c.

```
172  void qdisc_kill_estimator(struct tc_stats *stats)
173  {
174      int idx;
175      struct qdisc_estimator *est, **pest;
176
177      for (idx=0; idx<EST_MAX_INTERVAL; idx++) {
178          killed = 0;
179          pest = &elist[idx].list.list = NULL;
180          while ((*pest) != NULL) {
181              if (est->stats != stats) {
182                  pest = est->next;
183                  continue;
184              }
185              
186              write_lock_bb(&est_lock);
187              *pest = est->next;
188              write_unlock_bb(&est_lock);
189          }
190
191          kfree(est);
192          killed++;
193      }
194      if (killed && (p)->p->elist[idx].list == NULL)
195          del_timer(&elist[idx].timer);
196      }
197  }
```

**Here we see what the policer functions look like.**

**Figure 9.217** Policer i: linux/net/sched/police.c.

```
34  #define L2T(p,L) ((p)->R_tab->data(L)->p)->R_tab->rate.cell_log)
35  #define L2P(p,L) ((p)->P_tab->data(L)->p)->P_tab->rate.cell_log)
36
37  static u32 idx_gen;
38  static struct tcf *tcf_police_ht[16];
39  /* Policer hash table lock */
40  static rwlock_t police_lock = RW_LOCK_UNLOCKED;
41
42  /* Each policer is serialized by its individual spinlock */
```