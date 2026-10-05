

# 图 9.225 入站队列-树处理：linux/net/sched/sch_ingress.c。

```c
56 static int ingress_graft(struct Qdisc *sch, unsigned long arg,
57                              struct Qdisc *new,struct Qdisc *old)
58 {
59     #ifdef DEBUG_INGRESS
60         struct ingress_qdisc_data *p = PRIV(sch);
61     #endif
62 
63     DPRINTK("ingress_graft(sch %p,[qdisc %p],new %p,old %p)\n",
64             sch, p, new, old);
65     DPRINTK("\n ingress_graft: You cannot add qdiscs to classes");
66     return 1;
67 }
68 
70 static struct Qdisc *ingress_leaf(struct Qdisc *sch, unsigned long arg)
71 {
72     return NULL;
73 }
74 
76 static unsigned long int ingress_get(struct Qdisc *sch,u32 classid)
77 {
78     #ifdef DEBUG_INGRESS
79         struct ingress_qdisc_data *p = PRIV(sch);
80     #endif
81     DPRINTK("\ningress_get(sch %p,[qdisc %p],classid %x)\n", sch, p, classid);
82     return TC_R_MIN(classid) + 1;
83 }
84 
86 static unsigned long int ingress_bind_filter(struct Qdisc *sch,
87                               unsigned long parent,u32 classid)
88 {
89     return ingress_get(sch, classid);
90 }
91 
93 static void ingress_put(struct Qdisc *sch, unsigned long cl)
94 {
95 }
```

## 804 TCP/IP 与 Linux 协议实现

## 转发

图 9.226 入站队列-更改参数：linux/net/sched/sch_ingress.c。

```c
98 static int ingress_change(struct qdisc *sch, u32 classid, u32 parent,
99               struct rtattr **tca, unsigned long *arg)
100 {
101     #ifdef DEBUG_INGRESS
102     struct ingress_qdisc_data *p = PRIV(sch);
103     #endif
104     DPRINTK("ingress_change(sch %xp, [qdisc %xp],class %x, parent %x, %arg)",
105             arg%02lx\n", sch, p, classid, parent, arg);
106     DPRINTK("No effect, sch_ingress doesn't maintain classes at the moment");
107     return 0;
108 }
```

图 9.227 入站队列遍历树：linux/net/sched/sch_ingress.c。

```c
112 static void ingress_walk(struct qdisc *sch,struct qdisc_data *walker)
113 {
114     #ifdef DEBUG_INGRESS
115     struct ingress_qdisc_data *p = PRIV(sch);
116     #endif
117     DPRINTK("ingress_walk(sch %xp, [qdisc %xp].walker %xp)\n", sch, p, walker);
118     DPRINTK("No effect, sch_ingress doesn't maintain classes at the moment");
119 }
122 static struct tcf_proto **ingress_find_tcf(struct qdisc *sch,unsigned long cl)
123 {
125     struct ingress_qdisc_data *p = PRIV(sch);
126     return &p->filter_list;
127 }
```

图 9.228 入站队列入队：struct_qdisc:linux/net/sched/sch_ingress.c。

```c
133 static int ingress_enqueue(struct sk_buffer *skb,struct qdisc *sch)
134 {
135     struct ingress_qdisc_data *p = PRIV(sch);
136     struct tcf_result *res;
137     int result;
139     DPRINTK("ingress_enqueue(skb %xp, [qdisc %xp])\n", skb, sch);
140     result = tc_classify(skb, p->filter_list, &res);
142     /
143     DPRINTK("Xd class 0x%04x\n", result, classid);
144 /*
145     * 与普通的 "enqueue" 函数不同，ingress_enqueue 返回一个
146     * 防火墙 FW 码。
147     */
148     switch (result) {
149     #ifdef CONFIG_NET_CLS_POLICE
150         case TC_POLICY_SHOT:
149     result = NF_DROP;
150     break;
151     case TC_POLICE_RECLASSI: /* 此处标记 DSCP ? */
152     case TC_POLICE_OK:
153     case TC_POLICE_UNSPEC:
154     default:
155     result = NF_ACCEPT;
156     break;
157     #endif
158 };
159 
160     skb->tc_index = TC_H_MIN(res.classid);
161     return result;
162 }
```

## 图 9.229 入站队列-出队：linux/net/sched/sch.ingress.c。

```c
165 static struct sk_buff *ingress_dequeue(struct qdisc *sch)
166 {
167     /*
168 
169 struct ingress_qdisc_data *p = PIV(sch);
170 D2PRINTK("ingress_dequeue(sch xp, [qdisc xp])\n",sch,schb,PRIV(sch));
171 */
172 return NULL;
173 }
```

## 图 9.230 入站队列-重入：linux/net/sched/sch.ingress.c。

```c
175 static int ingress_requeue(struct sk_buff *skb,struct qdisc *sch)
176 {
177
178
179 struct ingress_qdisc_data *p = PIV(sch);
180 D2PRINTK("ingress_requeue(skb xp, [qdisc xp])\n",skb,sch,PRIV(sch));
181 return 0;
183 }
```

## 图 9.231 入站队列-丢弃：linux/net/sched/sch.ingress.c。

```c
184 static int ingress_drop(struct qdisc *sch)
185 {
186 #ifdef DEBUG_RX_INGRESS
187
188 struct ingress_qdisc_data *p = PIV(sch);
189 #endif
190 D2PRINTK("ingress_drop(sch xp, [qdisc xp])\n",sch, p);
191 return 0;
192 }
```

## 9.3.3 区分服务 (Differentiated Services)

区分服务基于数据标记。根据各种过滤器进行标记，然后根据行为进行处理。

### 9.3.2 区分服务标记数据：linux/net/sched/dms.c。

```c
30 #define PRIV(sch) ((struct dmsark_qdisc_data *)(sch)->data
31 
32 /*
33  * class       标记
34  * n/a
35  * x:0           使用项 [0]
36  * x:y           使用项 [y]
37  * indices     
38  * indices-1  使用项 [1]
39  */
40 
41 struct dmsark_qdisc_data {
42     struct qdisc         *q;
43     struct tcf_proto      *filter_list;
44     __u8                *mask;
45     __u8                *value;
46     __u16               indices;
47     __u16               default;
48 };
```

### 9.3.3 区分服务标记函数：linux/net/sched/sch_ingress.c。

```c
56 /* 操作 */
57 
58 static int dmsark_graft(struct qdisc *sch, unsigned long arg,
59                              struct Qdisc *new,struct Qdisc *old)
60 {
61     #ifdef DEBUG_INGRESS
62         struct ingress_qdisc_data *p = PRIV(sch);
63     #endif
64 
65     DPRINTK("ingress_graft(sch %p,[qdisc %p],new %p,old %p)\n",
66             sch, p, new, old);
67     DPRINTK("\n ingress_graft: You cannot add qdiscs to classes");
68     return 1;
69 static struct Qdisc *ingress_leaf(struct qdisc *sch, unsigned long arg)
70 {
71     return NULL;
72 } static unsigned long int ingress_get(struct qdisc *sch,u32 classid)
73 {
74     #ifdef DEBUG_INGRESS
75         struct ingress_qdisc_data *p = PRIV(sch);
76     #endif
77     DPRINTK("\ningress_get(sch %p,[qdisc %p],classid %x)\n", sch, p, classid);
78     return TC_R_MIN(classid) + 1;
79 } static unsigned long int ingress_bind_filter(struct Qdisc *sch,
80                               unsigned long parent,u32 classid)
81 {
82     return ingress_get(sch, classid);
83 } static void ingress_put(struct Qdisc *sch, unsigned long cl)
84 {
85 }
86 static int ingress_change(struct qdisc *sch, u32 classid, u32 parent,
87               struct rtattr **tca, unsigned long *arg)
88 {
89     #ifdef DEBUG_INGRESS
90         struct ingress_qdisc_data *p = PRIV(sch);
91     #endif
92     DPRINTK("ingress_change(sch %xp, [qdisc %xp],class %x, parent %x, %arg)",
93             arg%02lx\n", sch, p, classid, parent, arg);
94     DPRINTK("No effect, sch_ingress doesn't maintain classes at the moment");
95     return 0;
96 }
97 static void ingress_walk(struct qdisc *sch,struct qdisc_data *walker)
98 {
99     #ifdef DEBUG_INGRESS
100     struct ingress_qdisc_data *p = PRIV(sch);
101     #endif
102     DPRINTK("ingress_walk(sch %xp, [qdisc %xp].walker %xp)\n", sch, p, walker);
103     DPRINTK("No effect, sch_ingress doesn't maintain classes at the moment");
104 }
105 static struct tcf_proto **ingress_find_tcf(struct qdisc *sch,unsigned long cl)
106 {
107     struct ingress_qdisc_data *p = PRIV(sch);
108     return &p->filter_list;
109 }
110 static int ingress_enqueue(struct sk_buffer *skb,struct qdisc *sch)
111 {
112     struct ingress_qdisc_data *p = PRIV(sch);
113     struct tcf_result *res;
114     int result;
115     DPRINTK("ingress_enqueue(skb %xp, [qdisc %xp])\n", skb, sch);
116     result = tc_classify(skb, p->filter_list, &res);
117     /
118     DPRINTK("Xd class 0x%04x\n", result, classid);
119     /*
120     * 与普通的 "enqueue" 函数不同，ingress_enqueue 返回一个
121     * 防火墙 FW 码。
122     */
123     switch (result) {
124     #ifdef CONFIG_NET_CLS_POLICE
125         case TC_POLICY_SHOT:
126     result = NF_DROP;
127     break;
128     case TC_POLICE_RECLASSI: /* 此处标记 DSCP ? */
129     case TC_POLICE_OK:
130     case TC_POLICE_UNSPEC:
131     default:
132     result = NF_ACCEPT;
133     break;
134     #endif
135 };
136 
137     skb->tc_index = TC_H_MIN(res.classid);
138     return result;
139 }
140 static struct sk_buff *ingress_dequeue(struct qdisc *sch)
141 {
142     /*
143 
144 struct ingress_qdisc_data *p = PIV(sch);
145 D2PRINTK("ingress_dequeue(sch xp, [qdisc xp])\n",sch,schb,PRIV(sch));
146     */
147 return NULL;
148 }
149 static int ingress_requeue(struct sk_buff *skb,struct qdisc *sch)
150 {
151
152
153 struct ingress_qdisc_data *p = PIV(sch);
154 D2PRINTK("ingress_requeue(skb xp, [qdisc xp])\n",skb,sch,PRIV(sch));
155 return 0;
156 }
157 static int ingress_drop(struct qdisc *sch)
158 {
159 #ifdef DEBUG_RX_INGRESS
160
161 struct ingress_qdisc_data *p = PIV(sch);
162 #endif
163 D2PRINTK("ingress_drop(sch xp, [qdisc xp])\n",sch, p);
164 return 0;
165 }
```

