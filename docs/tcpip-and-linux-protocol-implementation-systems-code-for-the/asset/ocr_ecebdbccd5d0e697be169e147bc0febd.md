# Forwarding 741

```
1081  *ecf = 1;
1082
1083  return len;
1084 }
1085 #endif
1087  #if PSCHED_CLOCK_SOURCE == PSCHED_GETTIME_OFDAY
1088  int psched_tod_diff(int delta_sec, int bound)
1089 {
1091    int delta_sec;
1092    if (bound <= 1000000 || delta_sec > (0x7FFFFFFF/1000000)-1)
1093      return_bound;
1094      delta = delta_sec * 1000000;
1095      if (delta > bound)
1096        delta = bound;
1097      return_delta;
1098   }
1100  #endif

1101 psched_time_t psched_time_base;
1103  #if PSCHED_CLOCK_SOURCE == PSCHED_CPU
1104  psched_tdiff_t psched_clock_per_hz;
1105  int psched_clock_scale;
1106  #endif

1108  #ifdef PSCHED_WATCHER
1109  PSCHED_WATCHER psched_time_mark;
1110
1111  static void void psched_tick(unsigned long dummy)
1
1113  static struct timer_list psched_timer = =
1114    { function: psched_tick; };
```

Figure 9.116 Scheduler API-packet scheduling tick: linux/net/sched/sch_api.c.

```
1116 static void psched_tick(unsigned long dummy)
1118  #if PSCHED_CLOCK_SOURCE == PSCHED_CPU
1119    psched_time_t dummy_atamp;
1120    psched_GET_TIME(dummy_stamp);
1121    /* / if it is gr up to 400 cpu + */
1122    psched_timer.expires = jiffies + 1*HZ;
1123  #else
1124    unsigned long now = jiffies;
1125    psched_time_base = (u64)now<PSCHED_SCALE;
1126    psched_time_mark = now;
1127    psched_timer.expires = now + 60*60*HZ;
1128  #endif
1130    add_timer(&psched_timer);
1131  }
```