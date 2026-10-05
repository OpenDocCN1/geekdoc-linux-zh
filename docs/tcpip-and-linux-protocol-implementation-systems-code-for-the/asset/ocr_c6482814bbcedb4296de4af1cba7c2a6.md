# Figure 6.176 IGMP configure multicast interface: linux/net/ipv4/igmp.c.

```
128 static void ip_ma_put(struct ip_mc_list *im)
129 {
130 if (atomic_dec_and_test(im->refcnt)) {
131     in_dev_put(im->interface);
132     kfree(im);
133 }
134 }
```

# IGMP Timers to Manage State

# Figure 6.177 IGMP timer management: linux/net/ipv4/igmp.c.

```
142 static __inline_ void igmp_stop_timer(struct ip_mc_list *im)
143 {
144     spin_lock_bh(im->lock);
145     if (del_timer(im->timer)) {
146         atomic_dec(im->refcnt);
147         im->tm_running=0;
148         im->unsolicit_count=0;
149         spin_unlock_bh(im->lock);
150     }
151 }
152 
153     /* It must be called with locked im->lock */
154 void igmp_start_timer(struct ip_mc_list *im, int max_delay)
155 {
156     int tv=rand() % max_delay;
157 
158     im->tm_running=1;
159     if (!mod_timer(im->timer, jiffies+tv+2)) {
160         atomic_dec(im->refcnt);
161     }
162 }
163 void igmp_mod_timer(struct ip_mc_list *im, int max_delay)
164 {
165     spin_lock_bh(im->lock);
166     im->unsolicit_count=0;
167     if (del_timer(im->timer)) {
168         if ((long)(im->timer->expires-jiffies) < max_delay) {
169             add_timer(im->timer);
170             im->tm_running=1;
171             spin_unlock_bh(im->lock);
172             return;
173         }
174         atomic_dec(im->refcnt);
175     }
176     igmp_start_timer(im, max_delay);
177     spin_unlock_bh(im->lock);
178 }
```