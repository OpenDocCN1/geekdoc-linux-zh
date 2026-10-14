
```
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

# 图 9.237 Marker--find: linux/net/sched/sch_dmark.c.

```
166 static struct tcf_proto *dmaskark_find_tcf(struct qdisc *sch,unsigned long cl)

167 {

168     struct dmaskark_qdisc_data *p = PRIV(sch);

170     return &p->filter_list;

171 }
```

# 图 9.238 Marker--enqueue i: linux/net/sched/sch_dmark.c.

```
177 int dmask_enqueue(struct sk_buff *skb,struct qdisc *sch)

178 {

179     struct dmaskark_qdisc_data *p = PRIV(sch);

180     struct tcf_result *res;

181     int result;

182     int ret;

184     printk("dmask_enqueue(%p, %p, [qdisc %p])\n",skb,sch,p);

185     if (p->set_tc_index) {

186         switch (htons(skb->h->h_proto)) {

187             case constant_htons(ETH_P_IP):

188                 skb->tc_index = ipv4_get_dsfield(skb->nh);

189                 break;

190             case constant_htons(ETH_P_IPV6):

191                 skb->tc_index = ipv6_get_dsfield(skb->nh);

192                 break;

193             default:

194                 skb->tc_index = 0;

195                 break;

196         }

197     }

199 
```

# 图 9.239 Marker--enqueue ii: linux/net/sched/sch_dmark.c.

```
198 result = TC_POLICE_OK; /* 为了好性性 */

199 if (TC_H_MAX(skb->priority) == sch->priority) {

200     skb->tc_index = TC_H_MIN(skb->priority);

201 } else {

202     result = tcf_classify(skb,p->filter_list,res);

203     printk("Result %d Class 0x%04x\n",result,res->classid);

204     switch (result) {

205         #ifdef CONFIG_NET_CLS_POLICY
```
