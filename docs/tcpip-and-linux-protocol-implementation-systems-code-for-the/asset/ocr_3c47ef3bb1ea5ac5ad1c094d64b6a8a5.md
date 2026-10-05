# 696 TCP/IP and Linux Protocol Implementation

```
if (rvsp_get(tp, h) == 0)
    return h;
}
static int tunnel_bts(struct rvsp_head *data)
{
    int n = data->tgenerator>>5;
    u32 b = 1<<(data->tgenerator&0x1F);
    if (data->tmap[n]&b)
        return 0;
    data->tmap[n] |= b;
    return 1;
}
```

![](bbox=[0.135, 0.285, 0.815, 0.3])

```
static void tunnel_recycle(struct rvsp_head *data)
{
    struct rvsp_session **ht = data->ht;
    u32 tmap[256/32];
    int h1, h2;
    memset(tmap, 0, sizeof(tmap));
    for (hi=0; hi<256; hi++) {
        struct rvsp_session *s;
        for (s = ht[hi]; s = s->next) {
            for (h2=0; h2<16; h2++) {
                struct rvsp_filter *f;
                for (f = s->ht[h2]; f = f->next) {
                    if (f->tunnelhdr == 0)
                        continue;
                    data->tgenerator = f->res.classid;
                    tunnel_bts(data);
                }
            }
        }
    }
}
memcpy(data->tmap, tmap, sizeof(tmap));
static u32 gen_tunnel(struct rvsp_head *data)
{
    int i, k;
    for (k=0; k<2; k++) {
        for (i=255; i>0; i--) {
            if ((++data->tgenerator == 0
```