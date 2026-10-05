# Routing 577

458

459

  }

460

461

    memcpy(fi->&fib_prefarc, rta->rta_prefarc, 4);

462

Figure 8.42 FIB semantics-- FIB entry ii: linux/net/ipv4/fib.semantics.

```
if (rta->rta_mp) {
  #ifdef CONFIG_IP_ROUTE_MULTIPATH
    if ((err = fib_get_nbs(fi, rta->rta_mp, r)) != 0) {
      goto failures;
    }
    if (rta->rta_nh && fi->&fib_nh->oif != *rta->rta_oif) {
      goto err_inv;
    }
    if (rta->rta_gw && fi->&fib_nh->gw, rta->rta_gw, 4) {
      goto err_inv;
    }
  }
  #ifdef CONFIG_NET_CLS_ROUTE
    if (rta->rta_flow && fi->&fib_nh->nh_tclassid, rta->rta_flow, 4) {
      goto err_inv;
    }
  #endif
  else
    goto err_inv;
  #endif
} else {
  struct fib_nh *nh = fi->fib_nh;
  if (rta->rta_oif != *rta->rta_oif) {
    nh->nh_gw;
    memcpy(nh->&nh_gw, rta->rta_gw, 4);
  }
  #ifdef CONFIG_NET_CLS_ROUTE
    if (rta->rta_flow) {
      memcpy(nh->&nh_tclassid, rta->rta_flow, 4);
    }
  #endif
  nh->nh_flags = *rta->rtm_flags;
  #ifdef CONFIG_IP_ROUTE_MULTIPATH
    nh->nh_weight = 1;
  #endif
}
  #ifdef CONFIG_IP_ROUTE_NAT
  if (r->rtm_type == RTM_NAT) {
    if (rta->rta_gw == NULL || ! != 1 || *rta->rta_oif) {
      goto err_inv;
      memcpy(fi->&fib_nh->gw, rta->rta_gw, 4);
    }
    goto link_idx;
  }
  #endif
if (fib->props[r->rtm_type].error) {
  if (rta->rta_gw || rta->rta_oif || rta->rta_mp) {
    goto err_inv;
  }
  goto link_idx;
}
```