
# Infrastructure Protocols 263

```c
}
/* NB: cf RFC-1812 5.2.4.1 */
if (opt->*srr) {
    pp_ptr = optptr;
    goto error;
}
if (skb) {
    if (optptr[2] != 4 || optlen < 7 || ((optlen-3) & 3)) {
        pp_ptr = optptr + 1;
        goto error;
    }
    memcpy(&opt->faddr, &optptr[3], 4);
    if (optlen > 7) {
        memmove(&optptr[3], &optptr[7], optlen-7);
    }
    opt->is_stricture = (optptr[0] == IPOPT_SSRR);
    opt->srr = optptr - iph;
}
break;
```

Route record:

Figure 6.73 IP options-validate inbound packet header options: linux/net/ipv4/ip.options.c.

```c
case IPOPT_RR:
    if (opt->*srr) {
        pp_ptr = optptr;
        goto error;
    }
    if (optlen < 3) {
        pp_ptr = optptr + 1;
        goto error;
    }
    if (optptr[2] < 4) {
        pp_ptr = optptr + 2;
        goto error;
    }
    if (optptr[2]+3 <= optlen) {
        pp_ptr = optptr + 2;
        goto error;
    }
    if (skb) {
        memcpy(&optptr[optptr[2]-1], &rt->rt_spec_dest, 4);
        opt->is_changed = 1;
    }
    optptr[2] += 4;
    opt->*rr_neededaddr = 1;
}
opt->*rr = optptr - iph;
break;
```

# 264 TCP/IP and Linux Protocol Implementation

Timestamp option processing:

Figure 6.74 IP options-validate inbound packet header options: linux/net/ipv4/ip.options.c.

```c
case IPOPT_TIMESTAMP:
    if (opt->te) {
        pp_ptr = optptr;
        goto error;
    }
    if (optlen < 4) {
        pp_ptr = optptr + 1;
        goto error;
    }
    if (optptr[2] < 6) {
        pp_ptr = optptr + 2;
        goto error;
    }
    if (optptr[2] <= optlen) {
        __u32 * timeptr = NULL;
        if (optptr[2]+3 > optptr[1]) {
            pp_ptr = optptr + 2;
            goto error;
        }
        switch (optptr[3]&0xF) {
            case IPOPT_TS_TSONLY:
                opt->ts = optptr - iph;
                if (skb) {
                    timeptr = (__u32*)&optptr[2]-1);
                    opt->ts_needtime = 1;
                    optptr[2] += 4;
                    break;
                }
            case IPOPT_TS_TSANDANDOR:
                if (optptr[2]+7 > optptr[1]) {
                    pp_ptr = optptr + 2;
                    goto error;
                }
                opt->ts = optptr - iph;
                if (skb) {
                    memcpy(&optptr[2]-1], &rt->rt_spec_dest, 4);
                    timeptr = (__u32*)&optptr[2]+3);
                }
                opt->ts_needsaddr = 1;
                opt->ts_needtime = 1;
                optptr[2] += 8;
                break;
        }
```

# Figure 6.75 IP-validate inbound packet header options: linux/net/ipv4/options.c.

```c
382            case IPOPT_TS_PRESPEC:
383            if (optptr[2]+7 > optptr[1]) {
384                    pp_ptr = optptr + 2;
385                    goto error;
386                }
387            opt->ts = optptr - iph;
388            {
389                u32 addr;
390                memcpy(&addr, &optptr[optptr[2]-1], 4);
391                if (inst_add_type(addr) == RTN_UNICAST)
392                    break;
393                }
394                if (skb)
395                    timptr = ((u32*)optptr[optptr[2]+3];
396            }
397            opt->ts_needtime = 1;
398            optptr[2] += 8;
399            break;
400            default:
401                if (skb && !capable(CAP_NET_RAW)) {
402                    pp_ptr = optptr + 3;
403                    goto error;
404                }
405                break;
406            }
407            if (timptr) {
408                struct timeval tv;
409                u32 midtime;
410                do_gettimeofday(&tv);
411                midtime = htonl((tv.tv_sec % 86400) * 1000 + tv.tv_usec
412                / 1000);
413                memcpy(timptr, &midtime, sizeof(u32));
414                opt->is_changed = 1;
415            } else {
416                unsigned overflow = optptr[3]>>4;
417                if (overflow == 15) {
418                    pp_ptr = optptr + 3;
419                    goto error;
420                }
421                opt->ts = optptr - iph;
422                if (skb) {
423                    optptr[3] = (optptr[3]&0xF)|((overflow+1)<<4);
424                    opt->is_changed = 1;
425                }
426            }
427            break;
```

# 266 TCP/IP and Linux Protocol Implementation

Router alert handling:

Figure 6.76 IP options-end of options processing: linux/net/ipv4/ip_options.c.

```c
427             case IPOPT_RA:
428             if (optlen < 4) {
429                 pp_ptr = optptr + 1;
430                 goto error;
431             }
432             if (optptr[2] == 0 && optptr[3] == 0)
433                 opt_alert = optptr - iph;
434             break;
435             case IPOPT_SEC:
436             case IPOPT_SID:
437             default:
438                 if (skb && !capable(CAP_NET_RAW)) {
439                     pp_ptr = optptr;
440                     goto error;
441                 }
442             break;
443         }
444     optlen -= optlen;
445     optptr += optlen;
446 }
447 eol:
448     if (!pp_ptr)
449             return 0;
450     }
451 error:
452     if (skb) {
453         icmp_send(skb, ICMP_PARAMETER, 0, htons(pp_ptr-iph));
454     }
455     return -EINVAL;
456 }
```

Figure 6.77 IP options-undo what function did: linux/net/ipv4/ip_options.c.

```c
460     /*
461     Undo all the changes by ip_options_compile();
462     */
463 void ip_options_undo(struct ip_options *opt) {
464     {
465         if (opt->srr) {
466             unsigned char *optptr = opt->data+opt->rr-sizeof(struct iph);
467             memmove(optptr+7, optptr+3, optptr[7]);
468             memcpy(optptr+3, opt->faddr, 4);
469         }
470         if (opt->rraddr) {
471             unsigned char *optptr = opt->data+opt->rraddr-sizeof(struct iph);
```

# Infrastructure Protocols 267

```c
473    optptr[2] -= 4;
474    memset(&optptr[2]-1, 0, 4);
475    }
476    if (opt->ts) {
477        unsigned char *optptr = opt->data+opt->ts-sizeof(struct iph);
478        if (opt->ts_needtime) {
479            optptr[2] -= 4;
480            memset(&optptr[2]-1, 0, 4);
481            if ((optptr[3]&0xF) == IPOPT_TS_PRESPEC)
482                optptr[2] -= 4;
483        }
484        if (opt->ts_needaddr) {
485            optptr[2] -= 4;
486            memset(&optptr[2]-1, 0, 4);
487        }
488    }
```

Figure 6.78 IP options-make space for options: linux/net/ipv4/ip_options.c.

```c
491 int ip_options_get(struct ip_options **opt, unsigned char *data, int optlen, int user)
492 {
493     struct ip_options *opt;
494
495     opt = kmalloc(sizeof(struct ip_options)+((optlen+3)&3), GFP_KERNEL);
496     if (!opt) {
497         return -ENOMEM;
498         memset(opt, 0, sizeof(struct ip_options));
499         if (optlen) {
500             if (user) {
501                 if (copy_from_user(opt->_data, data, optlen)) {
502                     free(opt);
503                     return -EFAULT;
504                 }
505             } else {
506                 memcpy(opt->_data, data, optlen);
507             }
508             while (optlen & 3)
509                 opt->_data[optlen++] = IPOPT_END;
510             opt->optlen = optlen;
511             opt->is_byuser = 1;
512         }
513         if (opt && ip_options_compile(opt, NULL)) {
514             free(opt);
515             return -EINVAL;
516         }
517         *opt = opt;
518         return 0;
519     }
```

# Figure 6.79 IP options–forwarding options–for example, route record: linux/net/ipv4/ip.options.c.

```c
521 void ip_forward_options(struct sk_buff *skb)
522 {
523     struct ip_options *opt = &(IPCB(skb))->opt;
524     unsigned char *optpr;
525     struct rtable *rt = (struct rtable*)skb->nh_dst;
526     unsigned char *raw = skb->nh_raw;
527 
528 
529     if (opt->rr_neededaddr && (unsigned char*)raw + opt->rr) {
530         optpr = raw + opt->rr;
531         ip_rt_get_source(&optpr[optpr[2]-6], rt);
532         opt->is_changed = 1;
533     }
534     if (opt->rr_is_hit) {
535         int ssrptr, ssrspace;
536 
537         optpr = raw + opt->ts;
538         for (ssrptr = optpr[2], ssrspace = optpr[1]; ssrptr < ssrspace; ssrptr += 4) {
539             {
540                 if (ssrptr + 3 <= ssrspace)
541                     break;
542                     if (memcmp(&rt->rt_dest, &optpr[ssrptr-1], 4) == 0)
543                     break;
544                 }
545             }
546         if (ssrptr + 3 <= ssrspace) {
547             opt->is_changed = 1;
548             ip_rt_get_source(&optpr[ssrptr], rt);
549             skb->nh->ip_daddr = rt->rt_dest;
550             optpr[2] = ssrptr+4;
551         } else
552             printf(KERN_CRIT "ip_forward(): Arg! Destination lost!\n");
553             if (opt->is_neededaddr) {
554                 optpr = raw + opt->ts;
555                 ip_rt_get_source(&optpr[optpr[2]-9], rt);
556                 opt->is_changed = 1;
557             }
558     }
559     if (opt->is_changed) {
560         opt->is_changed = 0;
561         ip_send_check(skb->nh->iph);
562     }
563 }
```
