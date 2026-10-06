# 24.3 Connection Management

tcp_fin()
net/ipv4/tcp_input()

This function switches the TCP into the CLOSING state and sends a packet with the ACK flag set:

```
switch(sk->state) {
    (...)
    case TCP_FIN_WAIT1:
        tcp_send_ack(sk);
        tcp_set_state(sk, TCP_CLOSING);
    (...)
}
```

Transition from CLOSING to TIME_WAIT While the CLOSING state, TCP waits until it receives an ACK character. Subsequently, it switches into the TIME_WAIT state. (See Figure 24–9).

tcp_rcv_state_process()
net/ipv4/tcp_input()

```
if (th->ack) {
    switch(sk->state) {
        (...)
        case TCP_CLOSING:
            (...)
            tcp_time_wait(sk, TIME_WAIT, 0
            (...)
    }
}
```

**The TIME_WAIT** The different ways to tear down a connection all converge in the TIME_WAIT state. Computer A has to wait a specific period of time (twice the maximum segment lifecycle) before the connection is finally closed.

Additional functions are required to handle the TIME_WAIT state, and the special cases that can occur in this state, correctly.

_tcp_time_wait()
net/ipv4/tcp_minisocks.c

This function activates the TIME_WAIT state by initializing the tcp_tw_bucket structure and entering it in a hash table. As described earlier, this function is invoked by tcp_fin() when a connection changes to the TIME_WAIT state.

_tcp_tw_hashdance()
net/ipv4/tcp_minisocks.c

This function is a helper function of the tcp_time_wait function. It adds the tcp_tw_bucket structure to a hash table.