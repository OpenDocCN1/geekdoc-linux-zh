```
0,
NULL,                /* copy */   /* data */
    "Test_Protocol"      /* name */
;
int test_proto_rcv(struct sk_buff *skb)
{
    printk(KERN_DEBUG "Test protocol: Packet Received with length: %u\n",
           skb->len);
    return skb->len;
}
int init_module(void)
{
    inet_add_protocol(&test_protocol);
    return 0;
}
void cleanup_module(void)
{
    inet_del_protocol(&test_protocol);
}
```