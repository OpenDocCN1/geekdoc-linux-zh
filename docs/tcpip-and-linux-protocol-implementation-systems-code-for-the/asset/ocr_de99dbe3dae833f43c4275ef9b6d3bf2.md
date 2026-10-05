# 784 TCP/IP and Linux Protocol Implementation

```
1794    if (tb[TCA_CBQ_RATE-1]) &&
1795        RTA_PAYLOAD(tb[TCA_CBQ_RATE-1]) < sizeof(struct tc_ratespec)
1796            return -EINVAL;
1797
1798    if (tb[TCA_CBQ_LSSOPT-1]) &&
1799        RTA_PAYLOAD(tb[TCA_CBQ_LSSOPT-1]) < sizeof(struct tc_cbq_lsopt)
1800            return -EINVAL;
1801
1802    if (tb[TCA_CBQ_WRROPT-1]) &&
1803        RTA_PAYLOAD(tb[TCA_CBQ_WRROPT-1]) < sizeof(struct tc_cbq_wrropt)
1804            return -EINVAL;
1805
1806    #ifdef CONFIG_NET_CLS_POLICE
1807        if (tb[TCA_CBQ_POLICE-1]) &&
1808        RTA_PAYLOAD(tb[TCA_CBQ_POLICE-1]) < sizeof(struct tc_cbq_policy)
1809            return -EINVAL;
1810    #endif
1811
1812
1813    if (cl) {
1814        /* Check parent */
1815        if (parentid) {
1816            if (cl->tparent && cl->tparent->classid == parentid)
1817                return -EINVAL;
1818            if (!cl->tparent || cl->tparent->classid != TC_H_ROOT)
1819                return -EINVAL;
1820        }
1821    }
1822
1823    if (tb[TCA_CBQ_RATE-1]) {
1824        rtab = qdisc_get_rtab(RTA_DATA(tb[[TCA_CBQ_RATE-1]), tb[TCA_CBQ_RTAB-1]);
1825        if (rtab == NULL)
1826            return -EINVAL;
1827    }
```

# Figure 9.190 CBQ: linux/net/sched/sch.cbq.

```
1827    /* Change class parameters */
1828    sch_tree_lock(sch);
1829
1830    if (cl->next_alive != NULL)
1831        cbq_deactivate_class(cl);
1832
1833    if (rtab) {
1834        rtab = xchg(&cl->R_tab, rtab);
1835        qdisc_put_rtab(rtab);
1836        }
1837
1838    if (tb[TCA_CBQ_LSSOPT-1]) {
1839        cbq_set_ls(cl, RTA_DATA(tb[TCA_CBQ_LSSOPT-1]));
1840
1841    if (tb[TCA_CBQ_WRROPT-1]) {
1842        cbq_rmrio(q, cl);
1843        cbq_set_wrl(cl, RTA_DATA(tb[TCA_CBQ_WRROPT-1]));
1844    }
```