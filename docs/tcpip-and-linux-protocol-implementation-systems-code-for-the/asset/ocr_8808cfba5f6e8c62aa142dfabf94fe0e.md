# TCP/IP and Linux Protocol Implementation

```
481             skb_headerinit, NULL);
482     if (skbuff_head_cache)
483             panic("cannot create skbuff cache");
484
485     for (i=0; i<NR_CPUS; i++)
486                 skb_queue_head_init(&skb_head_pool[i].list);
487 }

```

# 5.7 A Day in the Life of a Protocol Control Block

Here is the relevant data for the protocol vis-à-vis the state of a stream-type socket in the INET protocol family.

5.1336 TCP states: linux/include/net/tcp.h

```
59      * Failing this, the port cannot be shared.
60      *
61      * The interesting point, is test #2. This is an FTP server does
62      * all day. As we optimize this case we use a specific flag been
63      * below: as we add sockets to a bind bucket list, we perform a
64              * check_of: (netsk->reuse_aa && (netsk->state == TCP_LISTEN));
65      * As long as all sockets are added to a bind bucket pass this test,
66      * the flag bit will be set.
67      * The resulting situation is that tcp_v4[4].verify_bind(bind) can just check
68      * for this flag, if it is set and the socket trying to bind
69      * sk-reuse is set, we don't have to walk the owners list at all,
70      * we return that it is ok to bind this socket to the requested local port.
71      *

72      * Sounds like a lot of work, but it is worth it. In a more naive
73      * implementation (i.e. FreeBSD etc.) the entry list of ports
74      * must be walked for each data port opened by an ftp server. Needless
75      * to say, this does not scale at all. With a couple thousand FTP
76      * users loaded onto your box, isn't nice to know that new data
77      * ports are created in O(1) time? I thought so. ;-)DaveM
78      */

79  struct tcp_bind_bucket {
80      unsigned short port;
81      unsigned short host;
82              struct fastreuse;
83              struct tcp_bind_bucket *next;
84              *owners;
85              struct sock
86              struct tcp_bind_bucket *pprev;
87  };

88  struct tcp_bind_hashbucket {
89      spinlock_t lock;
90              struct tcp_bind_bucket *chain;
91  };

```