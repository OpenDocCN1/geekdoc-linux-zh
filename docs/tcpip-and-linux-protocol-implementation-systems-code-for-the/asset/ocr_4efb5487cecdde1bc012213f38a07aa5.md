# Infrastructure Protocols 237

202

203

```
do {
    if (ipprot->protocol == iph->protocol) {
        struct sk_buff *skb2 = skb;
        if (ipprot->copy || force_copy)
            skb2 = skb_clone(skb, GFP_ATOMIC);
        if (skb2 == NULL) {
            ret = 1;
            ipprot->handler(skb, ntohts(iph->tot_len) - (iph->ihl * 4));
        }
    }
    ipprot = (struct inet_protocol *) ipprot->next;
} while (ipprot != NULL);
return ret;
```

204

205

206

207

208

209

210

211

212

213

214

215

216

217

218

![](bbox=[0.12875, 0.50625, 0.81125, 0.52437])

220 static inline ip_local_deliver_finish(struct sk_buff *skb)

{

```
struct iphdr *iph = skb->nh.iph;
```

221

222

223

```
#ifdef CONFIG_NETFILTER_DEBUG
deb_debug(ip_local_deliver(skb);
#endif // CONFIG_NETFILTER_DEBUG
```

224

225

226

227

> /* Point into the IP data, just past the header. */
skb->h.raw = skb->nh.raw + iph->ihl*4

228

229

230

231

> /* Note: See raw and net/raw, RAWV4_HTABLE_SIZE=MAX_INET_PROTOS */
hash int = iph->protocol & (MAX_INET_PROTOS - 1);
struct sock *sk = raw_v4_htable[hash];
struct inet_protocol *ipprot;
int flag;

232

233

234

235

236

237

> /* If there maybe a socket we must check - if not we
* don't care less
*/
if(raw_sk == NULL) {
    raw_sk = raw_v4_input(skb, iph, hash);
ipprot = (struct inet_protocol *) inet_protos[hash];
flag = 0;
}
if(ipprot != NULL) {
    if(raw_sk == NULL &&
        ipprot->next == NULL &&
        ipprot->protocol == iph->protocol)
        int ret;

238

239

240

241

242

243

244

245

246

247

248

249

250

251