# 10.3 Netfilter

# 10.3.1 Introduction

The netfilter code allows hooks to be placed in the packet flow. If we consider a Linux box acting as a router, then a hook can be placed at the following places (see Figure 10.6):

+   1. After input, before the routing stage (NF_IP_PRE_ROUTING)
2. After input if the packet is for the local machine (NF_IP_LOCAL_IN)
3. If the packet is to be forwarded (NF_IP_FORWARD)
4. Before the packet is output (NF_IP_POST_ROUTING)
5. If the packet is created locally (NF_IP_LOCAL_OUT)

Netfilter allows the following actions to be performed at a filtering hook:

+   - ACCEPT—Indicates that the packet should be allowed to continue; is, the next hook should be called.
- DROP—The packet should be dropped by the kernel.
- STEEL—The packet will be handled by another process.
- QUEUE—The packets should be queued for processing; usually this is to pass a packet to user space.
- REPEAT—Repeat the call to this hook.

![](bbox=[0.121, 0.673, 0.563, 0.903])

Figure 10.6 Possible hook locations.