yosemite_set_emacdata() function was not declared using the inline keyword, GCC inlined the function as a performance optimization.

# **Listing 14-9**

**Portions of Source File yosemite.c**

```
109 static void __init yosemite_set_emacdata(void)
110 {
111 struct ocp_def *def;
112 struct ocp_func_emac_data *emacdata;
113
114 /* Set mac_addr and phy mode for each EMAC */
115
116 def = ocp_get_one_device(OCV_VENDOR_IBM, OCV_FUNC_ENAC, 0);
117 emacdata = def->additions;
118 memcpy(&emacdata->mac_addr, __res.bi_enetaddr, 6);
119 emacdata->phy_mode = PHY_MODE_RMII;
120
121 def = ocp_get_one_device(OCV_VENDOR_IBM, OCV_FUNC_ENAC, 1);
122 emacdata = def->additions;
123 memcpy(&emacdata->mac_addr, __res.bi_enetladdr, 6);
124 emacdata->phy_mode = PHY_MODE_RMII;
125 }
126 ...
304
305 static void __init
306 yosemite_setup_arch(void)
307 {
308 yosemite_set_emacdata();
309
310 ibm440gx_get_clocks(&clocks, YOSEMITE_SYSCLK, 6 * 1843200);
311 ocp_sys_info.opb_bus_freq = clocks.opb;
312
313 /* init to some -safe value until calibrate_delay() runs */
314 loops_per_jif = 50000000/HZ;
315
316 /* Setup PCI host bridge */
317 yosemite_setup_hose();
318
319 #ifdef CONFIG_BLK_DEV_INITRD
320 if (initrd_start)
321 ROOT_DEV = Root_RAM0;
322 else
323 #endif
324 #ifdef CONFIG_ROOT_NFS
325 ROOT_DEV = Root_NFS;
326 #else
327 ROOT_DEV = Root_HDA1;
328 #endif
```