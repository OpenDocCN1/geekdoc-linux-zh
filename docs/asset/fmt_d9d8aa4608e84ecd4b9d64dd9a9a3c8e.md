
217 {
218     struct ip_fw ipfw;
219     struct ip_fwkernel *next;
220
221     struct ip_chain *branch;
222
223     int simplebranch;
224     struct ip_counters counters[0];
225 };
# IP 链 651
```c
net/ipv4/netfilter/ipchains_core.c
227 struct ip_reent
228 (
    struct ip_chain *prevchain;
    struct ip_fwkernel *prevrule;
    struct ip_counters counters;
232 );
```
cs 16.22. ipchains 的后指针管理。
```c
include/linux/netfilter_ipv4/ipchains_core.h
35 struct ip_fw
36 {
37    struct in_addr fw_src, fw_dst;
38    struct in_addr fw_msk, fw_dmsk;
39    u32 fw_mark;
40    u16 fw_proto;
41    u16 fw_fig;
42    u16 fw_infag;
43    u16 fw_spis[2];
44    u16 fw_dpts[2];
45    u16 fw_redirpt;
46    u16 fw_outputsize;
47;
48    char *fw_vianame[IFNAMSIZ];
49    u8 _u *fw_tosand, fw_tossxr;
50); };
```
cs 16.23. 规则的数据包匹配。
`ip_counters` 指向 `ip_fwkernel` 对象的结尾。在该结构的末尾，我们存储了一个 `ip_chains` 计数器对象。
为了获得更好的缓存局部性，每个 CPU 拥有这样一个对象。该对象记录了被过滤的数据包数量以及每个 IP 数据报中的字节数。

## 16.7.5 struct ip_reent
该结构在我们从当前链分支出去时（cs 16.22），保留了指向链和规则（rule）的后指针。这对于在分支链覆盖了所有过滤规则后，跳转回之前的链是必要的。该对象存储在 `ip_chain` 对象的末尾，其存在是为了满足 CPU 缓存局部性的目的。
- `prevchain` 是指向分支源链的后指针。
- `prevrule` 是指向在跳转回该链后，在该链上需要访问的下一个规则的指针。

## 16.7.6 struct ip_fw
该结构包含了过滤规则进行匹配所需的所有信息（cs 16.23）。
- `fw_dst` 和 `fw_src` 是目的地和源 IP 地址。
- `fw_msk` 和 `fw_dmsk` 是源和目的 IP 地址的掩码。
- `fw_proto_spts` 是 IP 头部中的协议字段，即 TCP/UDP。
- `fw_spts` 是要匹配的源端口地址范围。
- `fw_dpts` 是要匹配的目的端口地址范围。
- `fw_redirect` 是在需要时数据包重定向到的端口。
- `fw_vianame` 是防火墙规则要匹配的接口名称。
- `fw_invfltg` 是反转匹配规则的匹配实体标志。例如，如果匹配规则说是除源 IP 外的任何内容，那么 a.b.c.d 将在源 IP 上带有该标志。
- `fw_flg` 是指示结构中未提到的特殊匹配实体的标志，例如 SYN 数据包、分片规则等。

## 16.7.7 Ipchains 中表的组织
图 16.3 表示了链接在一起以实现 ip 链过滤的内核数据结构。
![](img/b3f231108facab5be0138b2cfd3f681a_668_0.png)

# 如何使用 IPCHAINS 过滤数据包

## 16.8 如何使用 IPCHAINS 过滤数据包
在节 16.7.2 中，我们看到 ip 链注册了三个 netfilter 钩子来过滤进入、输出和转发的数据包。处理这三种情况的通用例程是 `ip_fw_check()`。这是数据包通过所有过滤器并决定其包亡或命运的地方。让我们来看看它是如何实现的。

### 16.8.1 ip_fw_check()
我们有一个要过滤的数据包，以及传递给此例程的特定钩子的过滤链。我们需要保持扫描数据包，直到找到过滤规则的目标或结束对所有规则的扫描。我们在第 713 行（cs 16.24）访问过滤规则链。这里有两个循环。
- 外层循环让我们持续迭代（第 714–787 行），直到我们找到最终目标或完成了整个搜索且未找到目标（条件在第 787 行）。
- 内层循环遍历过滤规则链，只有当我们找到匹配规则，或者没有找到匹配规则且已完成对所有规则的扫描时（第 716–731 行），才会退出。
在处理链之前，我们需要做一些准备工作，例如提取 IP 地址、端口号、标志段、SYN 段等。
内层循环中的处理。我们遍历链中的过滤规则。在每次迭代中，我们通过调用第 718 行的 `ip_rule_match()` 来匹配规则。如果没有匹配规则，我们通过访问 `ip_fwkernel` 的下一个字段移动到链中的下一个规则。只有在覆盖了整个链或匹配了规则时，我们才跳出循环。
（由于原始文本存在大量 OCR 重复错误，此处已根据逻辑进行了清理并翻译）

`net/ipv4/netfilter/ipchains_core.c`
```c
281 static int ip_rule_match(struct ip_fwkernel *f,
282     const char *ifname,
283     struct iphdr *ip,
284     char *tip,
285     u16 src_port,u16 dst_port,
286     char isfrag)
287 {
288 #define FWIN(bool,bool) ((bool)(!f->fw_invflag & invlg))
295
296     if (FWIN(ip->saddr,f->fw_smks_addr) != f->fw_src_saddr) {
297         return IP_FW_INV_SRC;
298     if (FWIN(ip->dst_addr,f->fw_dmsk_addr) != f->fw_dst_saddr) {
300         return IP_FW_INV_DSTIP;
307
308         return 0;
311
     }
313     if (f->fw_flg &IP_flg & IP_FW_F_WILDIF) {
314         if (FWIN(strncmp(ifname,f->fw_vianame,
315             strlen(f->fw_vianame)) != 0)) {
316             return IP_FW_INV_VIAME;
317     }
319
320         return 0; /* Mismatch */
321     }
322     else if (FWIN(strncmp(ifname,f->fw_vianame))) {
323         return IP_FW_INV_VIA;
327
328         return 0; /* Mismatch */
329     }
336     if (FWIN(f->fw_flg&IP_FW_F_FRAG) && !isfrag) {
339         return IP_FW_INV_FRAG;
340     return 0;
341     }
343     if (FWIN(f->fw_flg&IP_FW_F_TCPSYN) && !tcpsyn) {
344         return IP_FW_INV_TCPSYN;
345     } || (isfrag && (!f->fw_flg&IP_FW_F_TCPSYN))) {
347
348         return 0;
349     }
350     if (ip->protocol!=f->fw_proto) {
356
357         if (FWIN(ip->protocol) != f->fw_proto) {
360             return 0;
361         }
364         if (port_match(ip->port,f->fw_ports[0],
365             f->fw_ports[1],
366             src_port, isfrag,
367             !(!f->fw_invflag&IP_FW_INV_SRCPT)) {
