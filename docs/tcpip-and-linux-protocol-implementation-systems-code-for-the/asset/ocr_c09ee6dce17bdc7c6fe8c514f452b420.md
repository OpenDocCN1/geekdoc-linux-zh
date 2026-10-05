# Infrastructure Protocols 279

```
454	tsk->protoinfo.af_inet.cmsg_flags |= IP_CMSG_TTL;
```

```
455	else
```

```
457	break;
```

```
458	case IP_RECTOS:
```

```
459	tif (val)
```

```
460	tsk->protoinfo.af_inet.cmsg_flags |= IP_CMSG_TOS;
```

```
461	else
```

```
462	tsk->protoinfo.af_inet.cmsg_flags &= ~IP_CMSG_TOS;
```

```
463	break;
```

```
464	case IP_RECVOPTS:
```

```
465	if (val)
```

```
466	tsk->protoinfo.af_inet.cmsg_flags |= IP_CMSG_RECVOPTS;
```

```
467	else
```

```
468	tsk->protoinfo.af_inet.cmsg_flags &= ~IP_CMSG_RECVOPTS;
```

```
469	break;
```

```
470	case IP_REPTOPTS:
```

```
471	if (val)
```

```
472	tsk->protoinfo.af_inet.cmsg_flags |= IP_CMSG_REPTOPTS;
```

```
473	else
```

```
474	tsk->protoinfo.af_inet.cmsg_flags &= ~IP_CMSG_REPTOPTS;
```

```
475	break;
```

Figure 6.96 IP socket-setsockopt entry for IP: linux/ipv4/ip.sockglue.c.

```
476	case IP_TOS: /* This sets both TOS and Precedence */
```

```
477	/* Reject setting of unused bits */
```

```
478\#ifndef CONFIG_INET_ECN
```

```
479	tif (val & (IPTOS_TOS_MASK|IPTOS_PREC_MASK))
```

```
480	goto e_inval;
```

```
482	if (sk->type == SOCK_STREAM) {
```

```
483	val &= ~3;
```

```
487	if (IPTOS_PREC(val) >= IPTOS_PREC_CRIT_ECP &&
```