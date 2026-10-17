
# TCP 参数列表

`tcp_conn_grace_period` (read and write)

`tcp_cwnd_max` (read and write)

`tcp_debug` (read and write)

`tcp_seack_last_nonpriv_port` (read and write)

`tcp_ip_abort_interval` (read and write)

`tcp_ip_abort_interval` (read and write)

`tcp_ip_abort_interval` (read and write)

`tcp_ip_notify_interval` (read and write)

`tcp_ip_notify_interval` (read and write)

`tcp_ip_ttl` (read and write)

`tcp_keepalive_interval` (read and write)

`tcp_maxsz_multiplier` (read and write)

`tcp_mss` (read and write)

`tcp_mss_max` (read and write)

`tcp_mss_min` (read and write)

`tcp_naglim_def` (read and write)

`tcp_retransmit_interval_initial` (read and write)

`tcp_retransmit_interval_min` (read and write)

`tcp_wroff_extra` (read and write)

`tcp_do_dup_ack_interval` (read and write)

`tcp_snd_lowat_fraction` (read and write)

`tcp_sth_rcv_hiwat` (read and write)

`tcp_sth_rcv_lowat` (read and write)

`tcp_dup_fast_retransmit` (read and write)

`tcp_ignore_path_mtu` (read and write)

`tcp_rcv_push_wait` (read and write)

`tcp_smallest_anon_port` (read and write)

`tcp_largest_anon_port` (read and write)

`tcp_xmit_max` (read and write)

`tcp_xmit_lowat` (read and write)

`tcp_recv_hiwat` (read and write)

`tcp_recv_hiwat_minmnss` (read and write)

`tcp_fin_wait_2_flush_interval` (read and write)

`tcp_co_min` (read and write)

`tcp_max_buf` (read and write)

`tcp_zero_win_probes` (read and write)

`tcp_strong` (read and write)

`tcp_retries` (read and write)

`tcp_wscale_always` (read and write)

`tcp_tstamp_always` (read and write)

`tcp_timewarp_initial` (read and write)

`tcp_retransmit_interval` (read and write)

`tcp_deferred_acks_max` (read and write)

`tcp_slow_after_idle` (read and write)

`tcp_slow_start_initial` (read and write)

`tcp_somconn_interval` (read and write)

`tcp_extra_priv_ports` (read only)

`tcp_extra_priv_ports_add` (write only)

`tcp_extra_priv_ports_del` (write only)

`tcp_status` (read only)

`tcp_bind_hash` (read only)

`tcp_list_hash` (read only)

`tcp_conn_hash` (read only)

`tcp_host_param` (read and write)

`tcp_pharse` (write only)

也可以为 IP 以及 TCP 设置参数。例如，如果 `ip_forwarding` 的值为 2（默认值），则它只在接口处于激活状态时执行路由。然而，如果此参数设置为 0，则 `ip_forwarding` 将永远不会执行（即确保多宿主配置）。可以通过以下命令设置：

```
ndd -set /dev/ip_forwarding 0
```
