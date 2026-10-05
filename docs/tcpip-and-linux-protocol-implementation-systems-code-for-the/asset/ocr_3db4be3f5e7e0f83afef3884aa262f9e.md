# TCP/IP and Linux Protocol Implementation

```
1005 static inline void sock_orphan(struct sock *sk)
1006 {
1007     write_lock_bb(sk->callback_lock);
1008     sk->dead = i;
1009     sk->socket = NULL;
1010     sk->sleep = NULL;
1011     write_unlock_bb(sk->callback_lock);
1012 }
```

Figure 1.514 Inline functions for socket reference management: linux/include/net/sock.h.

```
1014 static inline void sock_graft(struct sock *sk, struct socket *parent)
1015 {
1016     write_lock_bb(sk->callback_lock);
1017     sk->sleep = &parent->wait;
1018     parent->sk = sk;
1019     sk->socket = parent;
1020     write_unlock_bb(sk->callback_lock);
1021 }
1022
1023 static inline int sock_i_uid(struct sock *sk)
1024 {
1025     int uid;
1026
1027     read_lock(sk->callback_lock);
1028     uid = sk->socket->inode->i_uid ?: 0;
1029     read_unlock(sk->callback_lock);
1030     return uid;
1031 }
1032
1033 static inline unsigned long sock_i_ino(struct sock *sk)
1034 {
1035     unsigned long ino;
1036
1037     read_lock(sk->callback_lock);
1038     ino = sk->socket->inode->i_ino ?: 0;
1039     read_unlock(sk->callback_lock);
1040     return ino;
1041 }
```

# 5.7.4 Sockets and Routes

Next, we see the code to associate a socket with a route.

Figure 1.555 Route socket state management: linux/include/net/sock.h.

```
1043 static inline struct dst_entry *
1044     __sk_dst_get(struct sock *sk)
1045 {
1046     return sk->dst_cache;
```